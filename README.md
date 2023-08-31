import tkinter as tk

class CalculatorApp:
    def _init_(self, root):
        self.root = root
        self.root.title("Calculator")
        
        self.entry = tk.Entry(root, width=20, font=('Arial', 16))
        self.entry.grid(row=0, column=0, columnspan=4)
        
        self.create_buttons()
    
    def create_buttons(self):
        buttons = [
            ('7', 1, 0), ('8', 1, 1), ('9', 1, 2), ('/', 1, 3),
            ('4', 2, 0), ('5', 2, 1), ('6', 2, 2), ('*', 2, 3),
            ('1', 3, 0), ('2', 3, 1), ('3', 3, 2), ('-', 3, 3),
            ('0', 4, 0), ('.', 4, 1), ('=', 4, 2), ('+', 4, 3),
        ]
        
        for (text, row, col) in buttons:
            button = tk.Button(self.root, text=text, width=5, height=2, font=('Arial', 16),
                               command=lambda t=text: self.button_click(t))
            button.grid(row=row, column=col)
    
    def button_click(self, value):
        if value == '=':
            try:
                result = eval(self.entry.get())
                self.entry.delete(0, tk.END)
                self.entry.insert(0, str(result))
            except:
                self.entry.delete(0, tk.END)
                self.entry.insert(0, 'Error')
        else:
            current_text = self.entry.get()
            self.entry.delete(0, tk.END)
            self.entry.insert(0, current_text + value)

if _name_ == "_main_":
    root = tk.Tk()
    app = CalculatorApp(root)
    root.mainloop()
