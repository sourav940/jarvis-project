import speech_recognition as sr
import webbrowser
import pyttsx3 
import musiclibraray

recognizer = sr.Recognizer()
engine = pyttsx3.init()

def speak(text):
    engine.say(text)
    engine.runAndWait()

def process_command(command):
    if "open google" in command.lower():
        webbrowser.open("https://google.com")
    elif "open facebook" in command.lower():
        webbrowser.open("https://facebook.com")
    elif "open youtube" in command.lower():
        webbrowser.open("https://youtube.com")
    elif "open linkedin" in command.lower():
        webbrowser.open("https://linkedin.com")
    elif command.lower().startswith("play"):
        song = command.lower().split(" ")[1]
        link = musiclibraray.music[song]
        webbrowser.open(link)
        

if __name__ == "__main__":
    speak("Hello, I am Jarvis. How can I assist you Sourav?")
    while True:
        try:
            with sr.Microphone() as source:
                print("Listening...")
                audio = recognizer.listen(source, timeout=5)
            command = recognizer.recognize_google(audio)
            print("You said:", command)
            if command.lower() == "exit":
                speak("goodbye")
                break
            process_command(command)
        except Exception as e:
            print("Error:", e)
