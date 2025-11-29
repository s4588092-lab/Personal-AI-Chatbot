print("Namaste! Welcome to your personal chatbot")
print("You can ask me basic questions, type 'bye' to exit from the bot")

# chatbot memory (dictionary responses)
responses = {
    "hello": "Hi, welcome. How can I help you?",
    "how are you": "I am very fine. Thank you!",
    "who are you": "I am a smart AI chatbot.",
    "plz motivate me": "Keep going! Every bug in your project makes you a better developer.",
    "happy": "Great to hear that!",
    "functions kya hote hai": "Jaake chapter 7 padh le bhai!"
}

# function to get response of chatbot
def getResponseofBot(userQuestion):
    userQuestion = userQuestion.lower()

    for key in responses:
        if key in userQuestion:
            return responses[key]

    return "I am not able to answer that yet. I am still in learning mode."

# Take user input
while True:
    userInput = input("Please ask your question: ")
    reply = getResponseofBot(userInput)
    print("Bot Response:", reply)

    if "bye" in userInput.lower():
        print("Bot Response: Bye! Have a great day!")
        break
import tkinter as tk

# chatbot memory
responses = {
    "hello": "Hi, welcome. How can I help you?",
    "how are you": "I am very fine. Thank you!",
    "who are you": "I am a smart AI chatbot.",
    "plz motivate me": "Keep going! Every bug in your project makes you a better developer.",
    "happy": "Great to hear that!",
    "functions kya hote hai": "Jaake chapter 7 padh le bhai!",
}

# function to get bot response
def getResponseofBot(userQuestion):
    userQuestion = userQuestion.lower()
    for key in responses:
        if key in userQuestion:
            return responses[key]
    return "I am not able to answer that yet. I am still learning."

# send message function
def send_message():
    user_input = entry.get()
    if user_input.strip() == "":
        return

    chat_window.insert(tk.END, "You: " + user_input + "\n")
    entry.delete(0, tk.END)

    if "bye" in user_input.lower():
        chat_window.insert(tk.END, "Bot: Bye! Have a great day!\n")
        return

    reply = getResponseofBot(user_input)
    chat_window.insert(tk.END, "Bot: " + reply + "\n")

# GUI setup
root = tk.Tk()
root.title("AI Chatbot")
root.geometry("430x520")
root.resizable(False, False)

chat_window = tk.Text(root, height=25, width=50, font=("Arial", 12))
chat_window.pack(pady=10)

entry = tk.Entry(root, width=40, font=("Arial", 14))
entry.pack(side=tk.LEFT, padx=10)

send_button = tk.Button(root, text="Send", width=8, height=1, command=send_message)
send_button.pack(side=tk.LEFT)

root.mainloop()
import tkinter as tk
import speech_recognition as sr
import pyttsx3
import nltk
from nltk.stem import PorterStemmer

# Initialize NLP tools
stemmer = PorterStemmer()
nltk.download('punkt')

# Voice engine setup
engine = pyttsx3.init()
engine.setProperty("rate", 170)

def speak(text):
    engine.say(text)
    engine.runAndWait()

# Smart NLP matching
def nlp_match(user_input):
    user_words = nltk.word_tokenize(user_input.lower())
    user_stems = [stemmer.stem(word) for word in user_words]

    for key in responses:
        key_words = nltk.word_tokenize(key)
        key_stems = [stemmer.stem(word) for word in key_words]

        for stem in key_stems:
            if stem in user_stems:
                return responses[key]

    return "I don't fully understand yet, but I’m learning!"

# Chatbot memory
responses = {
    "hello": "Hi, welcome! How can I help you?",
    "how are you": "I am doing great! Thanks for asking.",
    "who are you": "I am your AI assistant chatbot.",
    "motivate": "Never give up! You are stronger than you think.",
    "happy": "That makes me happy too!",
    "sad": "I am here for you. Everything will be alright.",
    "bye": "Goodbye! Take care."
}

def take_voice_input():
    recognizer = sr.Recognizer()
    with sr.Microphone() as source:
        chat_window.insert(tk.END, "Listening...\n")
        root.update()
        audio = recognizer.listen(source)

    try:
        text = recognizer.recognize_google(audio)
        chat_window.insert(tk.END, "You (Voice): " + text + "\n")
        process_message(text)
    except:
        chat_window.insert(tk.END, "Bot: Sorry, I couldn't hear you clearly.\n")
        speak("Sorry, I couldn't hear you clearly.")

def process_message(user_input):
    chat_window.insert(tk.END, "You: " + user_input + "\n")

    if "bye" in user_input.lower():
        reply = "Goodbye! Have a great day!"
        chat_window.insert(tk.END, "Bot: " + reply + "\n")
        speak(reply)
        return

    reply = nlp_match(user_input)
    chat_window.insert(tk.END, "Bot: " + reply + "\n")
    speak(reply)

def send_text_message():
    user_input = entry.get()
    entry.delete(0, tk.END)
    process_message(user_input)

# ---------- GUI DESIGN ----------
root = tk.Tk()
root.title("AI Voice Chatbot")
root.geometry("500x600")
root.config(bg="#1e1e1e")

heading = tk.Label(root, text="AI Chatbot Assistant", font=("Arial", 18, "bold"), fg="white", bg="#1e1e1e")
heading.pack(pady=10)

chat_window = tk.Text(root, height=25, width=58, font=("Arial", 12), bg="#282828", fg="white")
chat_window.pack(pady=10)

entry = tk.Entry(root, width=33, font=("Arial", 14), bg="#3c3c3c", fg="white")
entry.pack(side=tk.LEFT, padx=10, pady=10)

send_btn = tk.Button(root, text="Send", font=("Arial", 12), command=send_text_message, bg="#00aaff", fg="white")
send_btn.pack(side=tk.LEFT, padx=5)

voice_btn = tk.Button(root, text="🎤 Speak", font=("Arial", 12), command=take_voice_input, bg="#ffaa00", fg="black")
voice_btn.pack(side=tk.LEFT, padx=5)

root.mainloop()
# main.py
from kivy.lang import Builder
from kivy.clock import mainthread
from kivy.core.window import Window
from kivy.utils import platform

from kivymd.app import MDApp
from kivymd.uix.boxlayout import MDBoxLayout
from kivymd.uix.button import MDIconButton, MDRaisedButton
from kivymd.uix.textfield import MDTextField
from kivymd.uix.label import MDLabel
from kivymd.uix.card import MDCard
from kivymd.uix.scrollview import MDScrollView

# TTS via plyer
from plyer import tts

# Attempt imports for Android speech (pyjnius)
ANDROID_AVAILABLE = False
if platform == "android":
    try:
        from jnius import autoclass, cast, PythonJavaClass, java_method
        ANDROID_AVAILABLE = True
    except Exception as e:
        ANDROID_AVAILABLE = False

import re
import threading

KV = '''
<ChatCard@MDCard>:
    size_hint_y: None
    padding: dp(8)
    md_bg_color: app.card_color
    radius: [10,]

BoxLayout:
    orientation: 'vertical'
    spacing: dp(8)
    padding: dp(8)

    MDLabel:
        text: "AI Voice Chatbot"
        halign: "center"
        font_style: "H5"
        size_hint_y: None
        height: self.texture_size[1] + dp(12)

    MDScrollView:
        id: scroll
        MDBoxLayout:
            id: messages
            orientation: 'vertical'
            size_hint_y: None
            height: self.minimum_height
            spacing: dp(8)
            padding: dp(4)

    BoxLayout:
        size_hint_y: None
        height: dp(56)
        spacing: dp(8)

        MDTextField:
            id: user_input
            hint_text: "Type your message..."
            mode: "rectangle"
            size_hint_x: 0.75

        MDRaisedButton:
            text: "Send"
            size_hint_x: 0.13
            on_release: app.on_send()

        MDRaisedButton:
            id: voice_btn
            text: "Speak"
            size_hint_x: 0.12
            on_release: app.on_voice()
'''

# -------------------------
# Simple NLP-style matcher (no external libs)
# -------------------------
def normalize(text):
    text = text.lower()
    text = re.sub(r'[^a-z0-9\s]', '', text)
    return text.strip()

def simple_stems(tokens):
    # very small stemming: remove common suffixes
    out = []
    for t in tokens:
        if len(t) > 5 and t.endswith('ing'):
            out.append(t[:-3])
        elif t.endswith('ed') and len(t) > 3:
            out.append(t[:-2])
        elif t.endswith('s') and len(t) > 2:
            out.append(t[:-1])
        else:
            out.append(t)
    return out

# chatbot memory
RESPONSES = {
    "hello": "Hi, welcome! How can I help you?",
    "how are you": "I am doing great! Thanks for asking.",
    "who are you": "I am your AI assistant chatbot.",
    "motivate": "Never give up! You are stronger than you think.",
    "happy": "That makes me happy too!",
    "sad": "I am here for you. Everything will be alright.",
    "function": "Functions are blocks of reusable code. Check chapter 7 for details!",
    "bye": "Goodbye! Take care."
}

def nlp_match(user_text):
    text = normalize(user_text)
    words = text.split()
    stems = simple_stems(words)

    # try exact phrase match first
    for key in RESPONSES.keys():
        if key in text:
            return RESPONSES[key]

    # token match using stems
    for key in RESPONSES.keys():
        key_tokens = normalize(key).split()
        key_stems = simple_stems(key_tokens)
        for k in key_stems:
            if k in stems:
                return RESPONSES[key]

    # fallback
    return "I don't fully understand yet, but I'm learning!"

# -------------------------
# Android Speech Recognizer wrapper (pyjnius)
# -------------------------
if ANDROID_AVAILABLE:
    # Android classes
    Context = autoclass('android.content.Context')
    PythonActivity = autoclass('org.kivy.android.PythonActivity')
    Intent = autoclass('android.content.Intent')
    RecognizerIntent = autoclass('android.speech.RecognizerIntent')
    SpeechRecognizer = autoclass('android.speech.SpeechRecognizer')

    class RecognitionListener(PythonJavaClass):
        __javainterfaces__ = ['android/speech/RecognitionListener']
        __javacontext__ = 'app'

        def __init__(self, callback):
            super().__init__()
            self.callback = callback

        @java_method('(Ljava/lang/CharSequence;)V')
        def onBeginningOfSpeech(self, s):
            pass

        @java_method('()V')
        def onBufferReceived(self, buff):
            pass

        @java_method('()V')
        def onEndOfSpeech(self):
            pass

        @java_method('(I)V')
        def onError(self, error):
            # call callback with None to indicate recognition error
            self.callback(None)

        @java_method('([Ljava/lang/String;F)V')
        def onEvent(self, p1, p2):
            pass

        @java_method('([Ljava/lang/String;)V')
        def onPartialResults(self, partial):
            pass

        @java_method('(Landroid/os/Bundle;)V')
        def onReadyForSpeech(self, bundle):
            pass

        @java_method('(Landroid/os/Bundle;)V')
        def onResults(self, results):
            # results is a Bundle; getStringArrayList via key "results_recognition"
            arr = results.getStringArrayList(RecognizerIntent.EXTRA_RESULTS)
            if arr.size() > 0:
                text = arr.get(0)
                self.callback(text)
            else:
                self.callback(None)

        @java_method('(ILandroid/os/Bundle;)V')
        def onRmsChanged(self, val, bundle):
            pass

# -------------------------
# App Definition
# -------------------------
class ChatApp(MDApp):
    card_color = [0.14, 0.14, 0.14, 1]

    def build(self):
        self.theme_cls.primary_palette = "Blue"
        self.root = Builder.load_string(KV)
        return self.root

    @mainthread
    def add_message(self, sender, text):
        msgs = self.root.ids.messages
        # create a small card per message
        card = MDCard(size_hint_y=None, padding=8, md_bg_color=self.card_color, radius=[10,])
        label = MDLabel(text=f"[b]{sender}:[/b]  {text}", markup=True, size_hint_y=None)
        # let label height adjust
        label.bind(texture_size=label.setter('size'))
        card.add_widget(label)
        card.height = label.texture_size[1] + 24
        msgs.add_widget(card)
        # scroll to bottom
        self.root.ids.scroll.scroll_y = 0

    def on_send(self):
        txt = self.root.ids.user_input.text.strip()
        if not txt:
            return
        self.root.ids.user_input.text = ""
        self.add_message("You", txt)
        # process in a thread so UI doesn't block
        threading.Thread(target=self.process_message, args=(txt,)).start()

    def on_voice(self):
        # If on Android and speech recognizer available, use it; else show message
        if ANDROID_AVAILABLE:
            threading.Thread(target=self.start_android_listen).start()
        else:
            self.add_message("Bot", "Voice input is available only on Android. Please type your message.")
            try:
                tts.speak("Voice input is available only on Android. Please type your message.")
            except Exception:
                pass

    def process_message(self, txt):
        # generate reply
        if "bye" in txt.lower():
            reply = RESPONSES.get("bye", "Goodbye!")
            self.add_message("Bot", reply)
            try:
                tts.speak(reply)
            except Exception:
                pass
            return

        reply = nlp_match(txt)
        self.add_message("Bot", reply)
        try:
            tts.speak(reply)
        except Exception:
            pass

    # Android-specific listening
    def start_android_listen(self):
        try:
            activity = PythonActivity.mActivity
            sr = SpeechRecognizer.createSpeechRecognizer(activity)
            listener = RecognitionListener(self.android_speech_callback)
            sr.setRecognitionListener(listener)
            intent = Intent(RecognizerIntent.ACTION_RECOGNIZE_SPEECH)
            intent.putExtra(RecognizerIntent.EXTRA_LANGUAGE_MODEL, RecognizerIntent.LANGUAGE_MODEL_FREE_FORM)
            intent.putExtra(RecognizerIntent.EXTRA_PROMPT, "Speak now...")
            sr.startListening(intent)
            # Note: SpeechRecognizer will call our listener asynchronously
        except Exception as e:
            self.add_message("Bot", "Failed to start voice recognizer.")
            try:
                tts.speak("Failed to start voice recognizer.")
            except Exception:
                pass

    @mainthread
    def android_speech_callback(self, text):
        if text is None:
            self.add_message("Bot", "Sorry, I couldn't hear you clearly.")
            try:
                tts.speak("Sorry, I couldn't hear you clearly.")
            except Exception:
                pass
        else:
            self.add_message("You (voice)", text)
            threading.Thread(target=self.process_message, args=(text,)).start()

if __name__ == "__main__":
    ChatApp().run()
[app]

title = AIVoiceChatbot
package.name = aivoicechat
package.domain = org.example
source.dir = .
source.include_exts = py,png,jpg,kv,atlas

# Python requirements - include plyer, kivy, kivymd, pyjnius
requirements = python3,kivy==2.1.0,kivymd,plyer,pyjnius

# (Optional) uncomment to include extra modules
# android.p4a_whitelist = ndk_platforms, ...

# Permissions
android.permissions = RECORD_AUDIO, INTERNET

# Add these so pyjnius and plyer are available
android.api = 33
android.minapi = 21
android.ndk = 25.

# orientation etc
orientation = portrait
buildozer init          # if you don't already have buildozer.spec
# Edit buildozer.spec as above
buildozer android debug deploy run

