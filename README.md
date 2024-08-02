# Phone Number Tracker

This project is a simple GUI application built using Python's `tkinter` library to track the country of a phone number using the `phone_country` function from the `phone_iso3166` library and `pycountry` for retrieving country information.

## Features

- Enter a phone number to track its country.
- Works in All Contries Including India
- The country information is displayed below the "Track Country" button.

## Installation

1. Clone the repository:

    ```sh
    git clone https://github.com/DevXOXUtkarsh/phone-number-tracker.git
    cd phone-number-tracker
    ```

2. Install the required libraries:

    ```sh
    pip install pycountry phone_iso3166
    ```

3. Run the application:

    ```sh
    python phone_number_tracker.py
    ```

## Code

```python
import pycountry
from tkinter import Tk, Label, Button, Entry
from phone_iso3166 import phone_country

class Location_Tracker:
    def __init__(self, App):
        self.window = App
        self.window.title("Phone Number Tracker")
        self.window.geometry("500x400")
        self.window.configure(bg="white")
        self.window.resizable(False, False)

        # Top section with saffron color
        self.top_frame = Label(App, bg="#FF9933", width=500, height=4)
        self.top_frame.place(x=0, y=0)

        # Middle section with white color
        Label(App, text="Enter a phone number", fg="black", font=("Times", 20), bg="white").place(x=150, y=60)
        self.phone_number = Entry(App, width=16, font=("Arial", 15), relief="flat")
        self.track_button = Button(App, text="Track Country", bg="#22c1c3", relief="sunken", command=self.Track_location)
        self.country_label = Label(App, fg="black", font=("Times", 20), bg="white")

        # Bottom section with green color
        self.bottom_frame = Label(App, bg="#138808", width=500, height=4)
        self.bottom_frame.place(x=0, y=370)

        # Place widgets on the window
        self.phone_number.place(x=170, y=140)
        self.track_button.place(x=200, y=220)
        self.country_label.place(x=100, y=300)

    def Track_location(self):
        phone_number = self.phone_number.get()
        country = "Indian Phone Number Tracker"
        if phone_number:
            try:
                tracked = pycountry.countries.get(alpha_2=phone_country(phone_number))
                if tracked:
                    country = getattr(tracked, 'official_name', tracked.name)
            except Exception as e:
                country = f"Error: {str(e)}"
        self.country_label.configure(text=country)

PhoneTracker = Tk()
MyApp = Location_Tracker(PhoneTracker)
PhoneTracker.mainloop()
```
