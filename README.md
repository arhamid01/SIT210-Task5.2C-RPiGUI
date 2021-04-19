# SIT210-Task5.2C-RPiGUI
from tkinter import *
import tkinter.font
from gpiozero import LED
import RPi.GPIO

RPi.GPIO.setmode(RPi.GPIO.BCM)

ledGreen = LED(18)
ledBlue = LED(10)
ledRed = LED(14)

window = Tk()
window.title("Press a button to turn on/off")
textFont = tkinter.font.Font(family = 'Calibri', size = 12) 

def toggleGreen():
    if ledGreen.is_lit:
        ledGreen.off()
        GreenButton["text"] = "Turn on green led"
    else:
        ledGreen.on()
        ledRed.off()
        ledBlue.off()
        GreenButton["text"] = "Turn off green led"

def toggleBlue():
    if ledBlue.is_lit:
        ledBlue.off()
        BlueButton["text"] = "Turn on blue led"
    else:
        ledBlue.on()
        ledRed.off()
        ledGreen.off()
        BlueButton["text"] = "Turn off blue led"

def toggleRed():
    if ledRed.is_lit:
        ledRed.off()
        RedButton["text"] = "Turn on red led"
    else:
        ledRed.on()
        ledBlue.off()
        ledGreen.off()
        RedButton["text"] = "Turn off red led"
        
def exit():
    RPi.GPIO.cleanup()
    window.destroy()
    
RedButton = Button(window, text = "Red LED ON", font = textFont, command = toggleRed, bg = 'red', height = 1, width = 25)
RedButton.grid(row=0, column=1)

BlueButton = Button(window, text = "Blue LED ON", font = textFont, command = toggleBlue, bg = 'blue', height = 1, width = 25)
BlueButton.grid(row=1, column=1)

GreenButton = Button(window, text = "Green LED ON", font = textFont, command = toggleGreen, bg = 'green', height = 1, width = 25)
GreenButton.grid(row=2, column=1)

ExitButton = Button(window, text = "Exit", font = textFont, command = exit, bg = 'yellow', height = 1, width = 25)
ExitButton.grid(row=3, column=1)
