import tkinter as tk
from tkinter import messagebox

class TodoApp:
    def __init__(self, root):
        self.root = root
        self.root.title("Lista de Tareas")
        self.root.geometry("400x400")

        self.tasks = []

        # Campo de entrada para nuevas tareas
        self.entry = tk.Entry(self.root, width=40)
        self.entry.pack(pady=10)
        self.entry.bind("<Return>", lambda event: self.add_task())

        # Botones de acciones
        self.add_button = tk.Button(self.root, text="Añadir Tarea", command=self.add_task)
        self.add_button.pack(pady=5)

        self.complete_button = tk.Button(self.root, text="Marcar como Completada", command=self.mark_completed)
        self.complete_button.pack(pady=5)

        self.delete_button = tk.Button(self.root, text="Eliminar Tarea", command=self.delete_task)
        self.delete_button.pack(pady=5)

        # Lista de tareas
        self.listbox = tk.Listbox(self.root, width=50, height=15, selectmode=tk.SINGLE)
        self.listbox.pack(pady=10)

    def add_task(self):
        task = self.entry.get()
        if task:
            self.tasks.append(task)
            self.listbox.insert(tk.END, task)
            self.entry.delete(0, tk.END)
        else:
            messagebox.showwarning("Advertencia", "La tarea no puede estar vacía.")

    def mark_completed(self):
        try:
            index = self.listbox.curselection()[0]
            task = self.listbox.get(index)
            self.listbox.delete(index)
            self.listbox.insert(index, f"✔ {task}")
        except IndexError:
            messagebox.showwarning("Advertencia", "Selecciona una tarea para marcarla.")

    def delete_task(self):
        try:
            index = self.listbox.curselection()[0]
            self.listbox.delete(index)
        except IndexError:
            messagebox.showwarning("Advertencia", "Selecciona una tarea para eliminarla.")

if __name__ == "__main__":
    root = tk.Tk()
    app = TodoApp(root)
    root.mainloop()
