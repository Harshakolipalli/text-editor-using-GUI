  Features
1.Create New File: Start a new text file and clear the current text area.
2.Open Existing File: Open a text file and load its content into the text area.
3.Save File: Save the current text area content to a file.
4.Exit: Close the application.
  Requirements
Python 3.x
Tkinter (usually included with Python installations)
  Installation
Clone the Repository:


git clone https://github.com/your-username/simple-text-editor.git
Navigate to the Project Directory:


cd simple-text-editor
Usage
Run the Application:


python simple_text_editor.py
Interact with the Application:

New: Click "File" -> "New" to create a new file.
Open: Click "File" -> "Open" to load an existing file.
Save: Click "File" -> "Save" to save the current text to a file.
Exit: Click "File" -> "Exit" to close the application.
Code Overview
SimpleTextEditor Class
__init__(self, root):

Initializes the application with a text area and a menu bar.
Adds options to the menu bar for creating, opening, saving files, and exiting the application.
new_file(self):

Clears the text area and sets the window title to "Untitled".
open_file(self):

Opens a file dialog to select a file, reads the file content, and loads it into the text area.
Updates the window title with the file path.
save_file(self):

Opens a file dialog to select the save location, writes the text area content to the file.
Updates the window title with the file path.
GUI Layout
Text Area: Where the user can enter and edit text.
Menu Bar: Contains options for "File" operations such as New, Open, Save, and Exit.
Example Code
Here is the main code for the text editor:

python
import tkinter as tk
from tkinter import filedialog, messagebox

class SimpleTextEditor:
    def __init__(self, root):
        self.root = root
        self.root.title("Simple Text Editor")

        # Create the text widget
        self.text_area = tk.Text(root, wrap='word')
        self.text_area.pack(expand='yes', fill='both')

        # Create the menu bar
        self.menu_bar = tk.Menu(root)
        root.config(menu=self.menu_bar)

        # Add File menu
        self.file_menu = tk.Menu(self.menu_bar, tearoff=0)
        self.menu_bar.add_cascade(label="File", menu=self.file_menu)
        self.file_menu.add_command(label="New", command=self.new_file)
        self.file_menu.add_command(label="Open", command=self.open_file)
        self.file_menu.add_command(label="Save", command=self.save_file)
        self.file_menu.add_command(label="Exit", command=root.quit)

    def new_file(self):
        """Create a new file and clear the text area."""
        self.text_area.delete(1.0, tk.END)
        self.root.title("Untitled - Simple Text Editor")

    def open_file(self):
        """Open an existing file and load its content into the text area."""
        file_path = filedialog.askopenfilename(defaultextension=".txt",
                                               filetypes=[("Text Files", "*.txt"), ("All Files", "*.*")])
        if file_path:
            with open(file_path, "r") as file:
                content = file.read()
                self.text_area.delete(1.0, tk.END)
                self.text_area.insert(tk.END, content)
                self.root.title(f"{file_path} - Simple Text Editor")

    def save_file(self):
        """Save the current text area content to a file."""
        file_path = filedialog.asksaveasfilename(defaultextension=".txt",
                                               filetypes=[("Text Files", "*.txt"), ("All Files", "*.*")])
        if file_path:
            with open(file_path, "w") as file:
                content = self.text_area.get(1.0, tk.END)
                file.write(content)
                self.root.title(f"{file_path} - Simple Text Editor")

 Create the main window
root = tk.Tk()
app = SimpleTextEditor(root)

 Run the application
root.mainloop()
  License
This project is licensed under the MIT License - see the LICENSE file for details.

  Contributing
If you wish to contribute to this project, please fork the repository and submit a pull request.
