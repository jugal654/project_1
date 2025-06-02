import requests
from kivy.app import App
from kivy.uix.boxlayout import BoxLayout
from kivy.uix.label import Label
from kivy.clock import Clock
from kivy.core.window import Window
from kivy.uix.image import Image
from kivy.graphics import Color, RoundedRectangle, Rectangle
import random
from datetime import datetime
from bs4 import BeautifulSoup
import re


class TopBar(BoxLayout):
    def __init__(self, **kwargs):
        super(TopBar, self).__init__(**kwargs)
        self.size_hint = (1, None)
        self.height = 50
        self.orientation = 'horizontal'
        self.padding = [10, 5]

        with self.canvas.before:
            Color(0.1, 0.1, 0.2, 1)  # Dark blue color
            self.rect = Rectangle(size=self.size, pos=self.pos)

        self.bind(pos=self.update_rect, size=self.update_rect)

        # Add content to the top bar
        self.title = Label(text=' Live Rates',
                           font_size='25sp',
                           bold=True,
                           color=(1, 1, 1, 1),
                           halign='center',
                           valign='middle')
        self.add_widget(self.title)

        # Add spacer to push time to right
        self.add_widget(Label(size_hint=(1, 1)))

        # Time in top bar
        self.time_label = Label(text='--',
                                font_size='14sp',
                                color=(1, 1, 1, 1),
                                halign='right',
                                valign='middle')
        self.add_widget(self.time_label)

    def update_rect(self, *args):
        self.rect.pos = self.pos
        self.rect.size = self.size

    def update_time(self, new_time):
        self.time_label.text = new_time


class RateCard(BoxLayout):
    def __init__(self, title, rate, icon, color, **kwargs):
        super(RateCard, self).__init__(**kwargs)
        self.orientation = 'horizontal'
        self.size_hint = (1, None)
        self.height = 100
        self.spacing = 20
        self.padding = [20, 10]
        self.previous_rate = 0  # Track previous rate for comparison
        self.is_increasing = False  # Track if rate is increasing

        with self.canvas.before:
            Color(*color)
            self.rect = RoundedRectangle(size=self.size, pos=self.pos, radius=[15])

        self.bind(pos=self.update_rect, size=self.update_rect)

        # Only add icon if one is provided
        if icon:
            self.icon = Image(source=icon, size_hint=(None, None), size=(60, 60))
            self.add_widget(self.icon)
        else:
            # Reduce spacing when no icon is present
            self.spacing = 0
            self.padding = [20, 10, 20, 10]

        # Rate info
        info_layout = BoxLayout(orientation='vertical', spacing=5)

        self.title_label = Label(text=title,
                                 font_size='18sp',
                                 bold=True,
                                 color=(1, 1, 1, 1),
                                 halign='left')
        self.rate_label = Label(text=rate,
                                font_size='24sp',
                                bold=True,
                                color=(1, 1, 1, 1),
                                halign='left')

        info_layout.add_widget(self.title_label)
        info_layout.add_widget(self.rate_label)
        self.add_widget(info_layout)

    def update_rect(self, *args):
        self.rect.pos = self.pos
        self.rect.size = self.size

    def update_rate(self, new_rate_str):
        # Extract numeric value from the rate string
        try:
            new_rate = int(''.join(filter(str.isdigit, new_rate_str)))

            # Compare with previous rate
            if new_rate > self.previous_rate:
                self.rate_label.color = (0, 1, 0, 1)  # Green for increasing
                self.is_increasing = True
            elif new_rate < self.previous_rate:
                self.rate_label.color = (1, 0, 0, 1)  # Red for decreasing
                self.is_increasing = False
            else:
                self.rate_label.color = (1, 1, 1, 1)  # White for no change
                self.is_increasing = False

            self.previous_rate = new_rate
            self.rate_label.text = new_rate_str
        except:
            # If parsing fails, just update the text
            self.rate_label.text = new_rate_str


class GoldSilverTracker(BoxLayout):
    def __init__(self, **kwargs):
        super(GoldSilverTracker, self).__init__(**kwargs)
        self.orientation = 'vertical'
        self.spacing = 10  # Reduced spacing
        self.padding = [0, 0, 0, 20]  # Adjusted padding

        # Initialize all components
        self.setup_ui()

        # Schedule updates
        self.setup_schedules()

    def setup_ui(self):
        # Clear existing widgets if any
        self.clear_widgets()

        # Store base rates for fluctuation
        self.base_gold_rate = 0
        self.base_adjusted_gold_rate = 0
        self.base_silver_rate = 0
        self.base_adjusted_silver_rate = 0
        self.base_adjusted_silver_rate_gst = 0

        # Set background color
        Window.clearcolor = (0.95, 0.95, 0.96, 1)

        # Add top bar
        self.top_bar = TopBar()
        self.add_widget(self.top_bar)

        # Main content layout
        content_layout = BoxLayout(orientation='vertical',
                                   spacing=20,
                                   padding=[30, 20, 30, 0])

        # Header with logo
        header_layout = BoxLayout(orientation='horizontal',
                                  size_hint=(1, None),
                                  height=80,
                                  spacing=20)

        # Title
        title_layout = BoxLayout(orientation='vertical')
        self.header = Label(text='Gayatri Jewellers',
                            font_size='30sp',
                            bold=True,
                            color=(0.5, 0.5, 0.4, 1))
        self.location_label = Label(text='For Nashik Maharashtra only',
                                    font_size='14sp',
                                    color=(0.4, 0.4, 0.4, 1))
        title_layout.add_widget(self.header)
        title_layout.add_widget(self.location_label)
        header_layout.add_widget(title_layout)

        content_layout.add_widget(header_layout)

        # Time and date (below header)
        self.time_label = Label(text='--',
                                font_size='14sp',
                                color=(0.5, 0.5, 0.5, 1))

        # Gold rate card
        self.gold_card = RateCard(
            title="Gold with GST% (per 10g)",
            rate="₹--",
            icon='',  # Empty string means no icon
            color=(0.1, 0.1, 0.2, 1)
        )
        content_layout.add_widget(self.gold_card)

        # Adjusted Gold rate card
        self.adjusted_gold_card = RateCard(
            title="24K Gold (per 10g)",
            rate="₹--",
            icon='',  # Empty string means no icon
            color=(0.1, 0.1, 0.2, 1)
        )
        content_layout.add_widget(self.adjusted_gold_card)

        # Adjusted Silver rate card (without GST)
        self.adjusted_silver_card = RateCard(
            title="Silver (per kilo)",
            rate="₹--",
            icon='',  # Empty string means no icon
            color=(0.1, 0.1, 0.2, 1)
        )
        content_layout.add_widget(self.adjusted_silver_card)

        # GST Silver rate card
        self.gst_silver_card = RateCard(
            title="Silver with GST% (per kilo)",
            rate="₹--",
            icon='',  # Empty string means no icon
            color=(0.1, 0.1, 0.2, 1)
        )
        content_layout.add_widget(self.gst_silver_card)

        # Footer
        footer = Label(text='Rates update every day stay connected\nData provided for Nashik city only',
                       font_size='12sp',
                       color=(0.5, 0.5, 0.5, 1))
        content_layout.add_widget(footer)

        self.add_widget(content_layout)

    def setup_schedules(self):
        # Cancel any existing schedules
        Clock.unschedule(self.update_rates)
        Clock.unschedule(self.simulate_fluctuation)
        Clock.unschedule(self.full_refresh)

        # Initial update
        self.update_rates()

        # Set up new schedules
        Clock.schedule_interval(lambda dt: self.update_rates(), 60)  # Update rates every 60 seconds
        Clock.schedule_interval(lambda dt: self.simulate_fluctuation(), 2)  # Fluctuate every 2 seconds
        Clock.schedule_interval(lambda dt: self.full_refresh(), 300)  # Full refresh every 5 minutes (300 seconds)

    def full_refresh(self):
        """Completely refresh the application"""
        print("\n=== Performing full refresh ===")
        self.setup_ui()
        self.setup_schedules()

    def fetch_gold_rate(self):
        try:
            url = "https://www.livemint.com/gold-prices"
            headers = {
                'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36'
            }
            page = requests.get(url, headers=headers, timeout=10)
            page.raise_for_status()

            soup = BeautifulSoup(page.content, 'html.parser')
            info = soup.find_all(class_="gpbox")

            if info:
                gold_text = info[0].get_text(strip=True)
                print("Original Gold Rate Text:", gold_text)

                # Extract numeric value using regex
                match = re.search(r'\₹\s?([\d,]+)', gold_text)
                if match:
                    gold_rate_str = match.group(1).replace(',', '')
                    gold_rate = int(gold_rate_str)
                    adjusted_gold_rate = gold_rate - 1593
                    gstrate = adjusted_gold_rate + 2000

                    print("Original 24 Carat Gold Rate: ₹{:,.0f}".format(gold_rate))
                    print("Original 24 Carat GST Rate: ₹{:,.0f}".format(gstrate))
                    print("Gold Rate After ₹1443 Decrease: ₹{:,.0f}".format(adjusted_gold_rate))
                    return gold_rate, adjusted_gold_rate
                else:
                    print("Could not extract the numeric gold rate.")
                    return None, None
            else:
                print("Could not find gold rate element on the page.")
                return None, None

        except requests.RequestException as e:
            print(f"Request failed: {e}")
            return None, None
        except Exception as e:
            print(f"An error occurred: {e}")
            return None, None

    def fetch_silver_rate(self):
        try:
            url = "https://www.livemint.com/silver-prices"
            headers = {
                'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36'
            }
            page = requests.get(url, headers=headers, timeout=10)
            page.raise_for_status()

            soup = BeautifulSoup(page.content, 'html.parser')
            info = soup.find_all(class_="gpBox silver")

            if info:
                silver_text = info[0].get_text(strip=True)
                print("Original Silver Rate Text:", silver_text)

                # Extract numeric value using regex
                match = re.search(r'\₹\s?([\d,]+)', silver_text)
                if match:
                    silver_rate_str = match.group(1).replace(',', '')
                    silver_rate = int(silver_rate_str)
                    adjusted_silver_rate = silver_rate * 100 - 4000  # Adjusted rate calculation
                    adjusted_silver_rate_gst = silver_rate * 100 - 3400  # GST rate calculation

                    print("Original Silver Rate: ₹{:,.0f}".format(silver_rate))
                    print("Adjusted Silver Rate (with making charges): ₹{:,.0f}".format(adjusted_silver_rate))
                    print("Adjusted Silver Rate (with GST): ₹{:,.0f}".format(adjusted_silver_rate_gst))
                    return silver_rate, adjusted_silver_rate, adjusted_silver_rate_gst
                else:
                    print("Could not extract the numeric silver rate.")
                    return None, None, None
            else:
                print("Could not find silver rate element on the page.")
                return None, None, None

        except requests.RequestException as e:
            print(f"Request failed: {e}")
            return None, None, None
        except Exception as e:
            print(f"An error occurred: {e}")
            return None, None, None

    def update_rates(self):
        try:
            # Update time
            now = datetime.now()
            time_str = now.strftime('%I:%M:%S %p')
            date_str = now.strftime('%A, %d %B %Y')

            # Update time in both places
            self.time_label.text = date_str + '\n' + time_str
            self.top_bar.update_time(time_str)

            # Fetch gold rates
            gold_rate, adjusted_gold_rate = self.fetch_gold_rate()

            # Update gold rates if fetched successfully
            if gold_rate is not None and adjusted_gold_rate is not None:
                self.base_gold_rate = gold_rate
                self.base_adjusted_gold_rate = adjusted_gold_rate
                self.gold_card.update_rate(f"₹{gold_rate:,}")
                self.adjusted_gold_card.update_rate(f"₹{adjusted_gold_rate:,}")

            # Fetch silver rates
            silver_rate, adjusted_silver_rate, adjusted_silver_rate_gst = self.fetch_silver_rate()

            # Update silver rates if fetched successfully
            if silver_rate is not None:
                self.base_silver_rate = silver_rate * 100  # Store the base rate
                self.base_adjusted_silver_rate = adjusted_silver_rate  # Store the adjusted rate
                self.base_adjusted_silver_rate_gst = adjusted_silver_rate_gst  # Store GST rate

                # Update silver cards
                self.adjusted_silver_card.update_rate(f"₹{adjusted_silver_rate:,}")  # Show adjusted rate
                self.gst_silver_card.update_rate(f"₹{adjusted_silver_rate_gst:,}")  # Show GST rate

        except Exception as e:
            self.time_label.text = f'Error updating rates: {str(e)}'

    def simulate_fluctuation(self):
        """Simulate small fluctuations in the rates"""
        try:
            # Gold fluctuation
            if self.base_gold_rate > 0:
                gold_fluctuation = random.randint(+100, 700)
                gstrate = self.base_gold_rate + gold_fluctuation
                self.gold_card.update_rate(f"₹{gstrate:,}")

                adjusted_gold_fluctuation = random.randint(-200, 200)
                current_adjusted_gold = self.base_adjusted_gold_rate + adjusted_gold_fluctuation
                self.adjusted_gold_card.update_rate(f"₹{current_adjusted_gold:,}")

            # Silver fluctuation
            if self.base_silver_rate > 0:
                # Adjusted rate fluctuates with the same pattern
                adjusted_fluctuation = random.randint(-50, 200)
                current_adjusted = self.base_adjusted_silver_rate + adjusted_fluctuation
                self.adjusted_silver_card.update_rate(f"₹{current_adjusted:,}")

                # GST rate fluctuates with the same pattern
                gst_fluctuation = random.randint(-100, 200)
                current_gst = self.base_adjusted_silver_rate_gst + gst_fluctuation
                self.gst_silver_card.update_rate(f"₹{current_gst:,}")

        except Exception as e:
            print(f"Error in fluctuation simulation: {e}")


class NashikRatesApp(App):
    def build(self):
        self.title = 'Gayatri Jewellers'
        return GoldSilverTracker()


if __name__ == '__main__':
    NashikRatesApp().run()