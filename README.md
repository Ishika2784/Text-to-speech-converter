# Text-to-speech-converter
from tkinter import *
from gtts import gTTS
from playsound import playsound
import os

# Function to convert text to speech
def text_to_speech():
    message = entry.get()
    if message:
        try:
            speech = gTTS(text=message, lang='en')
            speech.save("output.mp3")
            playsound("output.mp3")
            os.remove("output.mp3")  # Clean up the audio file after playing
        except Exception as e:
            error_label.config(text=f"Error: {str(e)}", fg="red")

# Function to reset the entry field
def reset_text():
    entry.delete(0, END)
    error_label.config(text="")

# Function to exit the application
def exit_app():
    root.destroy()

# Initialize Tkinter window
root = Tk()
root.title("CONVERT TEXT_TO_SPEECH")
root.geometry("400x300")

# Main label
main_label = Label(root, text="TEXT_TO_SPEECH", font=("Arial", 20, "bold"))
main_label.pack(pady=10)

# Label for entry box
entry_label = Label(root, text="Enter Text", font=("Arial", 14))
entry_label.pack(pady=5)

# Entry box for text input
entry = Entry(root, width=50)
entry.pack(pady=5)

# Frame for buttons
button_frame = Frame(root)
button_frame.pack(pady=10)

# Play button
play_button = Button(button_frame, text="PLAY", command=text_to_speech, font=("Arial", 14))
play_button.grid(row=0, column=0, padx=10)

# Exit button
exit_button = Button(button_frame, text="EXIT", command=exit_app, font=("Arial", 14), bg="red")
exit_button.grid(row=0, column=1, padx=10)

# Reset button
reset_button = Button(button_frame, text="RESET", command=reset_text, font=("Arial", 14))
reset_button.grid(row=0, column=2, padx=10)

# Error label
error_label = Label(root, text="", font=("Arial", 12))
error_label.pack(pady=5)

# Footer label
footer_label = Label(root, text="Ishika", font=("Arial", 12))
footer_label.pack(side=BOTTOM, pady=10)

# Run the Tkinter event loop
root.mainloop()
