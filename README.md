# BT.
# URL of the image to colorize
image_url = "https://example.com/image.jpg"

# Load the image from the URL
response = requests.get(image_url)
image = cv2.imdecode(np.frombuffer(response.content, np.uint8), -1)

# Convert the image to grayscale
gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

# Apply a contour drawing effect
contour_image = cv2.medianBlur(gray_image, 5)

# Set the brush thickness
thickness = 2

# Function to colorize drawing with the mouse
def colorize_drawing(event, x, y, flags, param):
    global image, color
    if event == cv2.EVENT_LBUTTONDOWN:
        cv2.circle(image, (x, y), thickness, color, -1)

# Function to choose the color
def choose_color():
    global color
    _, color = colorchooser.askcolor(title="Choose a color")

# Create the window and associate the colorization function with the mouse event
cv2.namedWindow('Colorize Drawing')
cv2.setMouseCallback('Colorize Drawing', colorize_drawing)

# Create a Tkinter window to display the color selection
root = tk.Tk()
color_button = tk.Button(root, text="Choose color", command=choose_color)
color_button.pack()

# Main loop
while True:
    cv2.imshow('Colorize Drawing', image)
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break

# Close the window when exiting the loop
cv2.destroyAllWindows()

# Load the HTML file with the 3D interface
with open('index.html', 'r') as file:
    html_content = file.read()

# Create a WebView window to display the 3D interface
webview.create_window('3D Editor', html=html_content, width=800, height=600)

# Execute the event loop of the WebView window
webview.start()
import cv2
import numpy as np
import tkinter as tk
from tkinter import colorchooser

# Define the URL of the image to colorize
image_url = "https://example.com/image.jpg"

# Load the image from the URL
response = requests.get(image_url)
image = cv2.imdecode(np.frombuffer(response.content, np.uint8), -1)

# Convert the image to grayscale
gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

# Apply a contour drawing effect
contour_image = cv2.medianBlur(gray_image, 5)

# Set the brush thickness
thickness = 2

# Function to colorize drawing with the mouse
def colorize_drawing(event, x, y, flags, param):
    global image, color
    if event == cv2.EVENT_LBUTTONDOWN:
        cv2.circle(image, (x, y), thickness, color, -1)

# Function to choose the color
def choose_color():
    global color
    _, color = colorchooser.askcolor(title="Choose a color")

# Create the Tkinter window
window = tk.Tk()
window.title("Colorize Drawing")

# Create the canvas to display the image
canvas = tk.Canvas(window, width=image.shape[1], height=image.shape[0])
canvas.pack()

# Convert the OpenCV image to the format supported by Tkinter
image_tk = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)
image_tk = Image.fromarray(image_tk)

# Display the image on the canvas
image_id = canvas.create_image(0, 0, anchor=tk.NW, image=image_tk)

# Associate the colorization function with the mouse event
canvas.bind("<Button-1>", colorize_drawing)

# Create the button to choose the color
color_button = tk.Button(window, text="Choose color", command=choose_color)
color_button.pack()

# Main loop
while True:
    # Update the image displayed on the canvas
    image_tk = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)
    image_tk = Image.fromarray(image_tk)
    canvas.itemconfig(image_id, image=image_tk)

    # Update the window
    window.update()

    # Exit the loop if the 'q' key is pressed
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break

# Close the window when exiting the loop
window.destroy()
