# **Proyecto 3 - Editor de texto con interfaz gráfica Tkinter**

**Proyecto desarrollado por**

*Roberto Antonio Ramírez Gómez 7690-22-12700*

## Enlace del video explicando el proceso del desarrolo del proyecto
[Video explicado el desarrolo del proyecto](https://youtu.be/CgpjSY9SuNM)
# *Documentación externa*

## Importamos Librerias
Primero importamos las librerias necesarias para que nuestra aplicación funcione correctamente.
## *Librerias*
~~~py
import tkinter as tk
from tkinter import scrolledtext as st
from tkinter import filedialog as fd
from tkinter import messagebox as mb
import os
~~~  

- **tkinter** es la libreria que nos permite crear una aplicacion con interfaz gráfica, mediante sus funciones **scrolledtext** **filedialog** **messagebox** nos permite darle un buen diseño al programa.
- **os** nos permite abrir archivos *pdf* o *paginas web*

## Creamos Clase

Creamos una clase llamada aplicación, en la cual definimos nuestro objeto app de tipo tk.Tk

Le colocamos titulo a nuestra aplicación

Llamanos a la funcion agregar

Definimos el tamaño de nuestra aplicación 

~~~py
class aplicacion:
    def __init__(self):
        self.app=tk.Tk()
        self.app.title("Editor de texto - Proyecto 3")
        self.menu()
        self.scrolledtext1=st.ScrolledText(self.app, width=70, height=20, undo=True, font=("Comic Sans MS", 12) )
        self.scrolledtext1.grid(padx=5, pady=3)      
        self.app.mainloop()
~~~

## Menu de la aplicación
Creamos nuestro menu principal dentro de la aplicación con los *label* y todos llaman a las funciones necesarias para que funcionen correctamente.

~~~py
    def menu(self):
        barramenu = tk.Menu(self.app)
        self.app.config(menu=barramenu)
        menuarchivo = tk.Menu(barramenu, tearoff=0)
        menueditar = tk.Menu(barramenu, tearoff=0)
        menuayuda = tk.Menu(barramenu, tearoff=0)
        menuarchivo.add_command(label="Nuevo", command=self.nuevo)
        menuarchivo.add_command(label="Abir", command=self.abrir)
        menuarchivo.add_command(label="Guardar", command=self.guardar)
        menuarchivo.add_command(label="Guardar como", command=self.guardarcomo)
        menuarchivo.add_separator()
        menuarchivo.add_command(label="Salir", command=self.app.destroy)
        barramenu.add_cascade(label="Archivo", menu=menuarchivo)
        #menueditar.add_command(label="Deshacer", command=self.deshacer)
        #menueditar.add_command(label="Rehacer", command=self.rehacer)
        menueditar.add_command(label="Deshacer")#, command=self.texto.edit_undo
        menueditar.add_command(label="Rehacer")#, command=self.texto.edit_redo
        menueditar.add_separator()
        menueditar.add_command(label="Borrar Todo", command=self.borrar)
        barramenu.add_cascade(label="Editar", menu=menueditar)
        menuayuda.add_command(label="Información, command=self.licencia)
        menuayuda.add_command(label="Manual de usuario", command=self.manual)
        menuayuda.add_command(label="Integrantes", command=self.integrantes)
        barramenu.add_cascade(label="Ayuda", menu=menuayuda)
~~~
## Funciones
### Función guardar

Esta funcion nos permite guardar guardar el archivo con el nombre y la carpeta que nosotros eligamos, atraves del parametro asksaveasfilename no permitira guardar el tipo de archivo que nosotros deseemos, con las tuplas .txt y *.* podremos escoger el tipo de archivo.
~~~py
    def guardar(self):
        nombrearchivo=fd.asksaveasfilename(initialdir = "/",title = "Guardar",filetypes = (("txt files","*.txt"),("todos los archivos","*.*")))
        if nombrearchivo!='':
            archivo=open(nombrearchivo, "w", encoding="utf-8")
            archivo.write(self.texto.get("1.0", tk.END))
            archivo.close()
            mb.showinfo("Información", "Los datos fueron guardados en el archivo.")
~~~
### Función abrir
Esta función nos permite abrir un archivo y editarlo. Con el parametro *askopemfilename* abrimos la ruta de los archivos y con las tuplas .txt y *.* podremos clasificar los tipos de archivos. Con el parametro scrolledtext1 podremos limpiar la pantalla y agregar todo el texto que contenga el archivo que deseamos abrir.
~~~py
    def abrir(self):
        nombrearchivo=fd.askopenfilename(initialdir = "/",title = "Seleccione archivo",filetypes = (("txt files","*.txt"),("todos los archivos","*.*")))
        if nombrearchivo!='':
            archivo=open(nombrearchivo, "r", encoding="utf-8")
            contenido=archivo.read()
            archivo.close()
            self.texto.delete("1.0", tk.END) 
            self.texto.insert("1.0", contenido)
~~~
Función guardacomo
Esta función nos permitira guardar una copia del archivo con el nombre y tipo de archivo que nosotros escojamos.
~~~py
    def guardarcomo(self): 
        nombrearchivo=fd.asksaveasfilename(initialdir = "/",title = "Guardar como",filetypes = (("txt files","*.txt"),("todos los archivos","*.*")))
        if nombrearchivo!='':
            archivo=open(nombrearchivo, "w", encoding="utf-8")
            archivo.write(self.texto.get("1.0", tk.END))
            archivo.close()
            mb.showinfo("Información", "Archivo guardado correctamente")
~~~

### Función borrar y nuevo
Simplemente borra todo el contenido que hay en la pantalla.

Con el parametro **scrolledtext1** nos permite borrar todo el contenido desde el primer caracter hasta el último.
~~~py
def borrar(self):
        self.texto.delete("1.0", tk.END)
def nuevo(self):
        self.texto.delete("1.0", tk.END)
~~~

### Funciones manual, licencia e integrantes
Estas funciones, mediante las librerias **os** y **messagebox as md** nos permite mostrar el manual de usuario, la licencia de la aplicación y los integrantes que desarrollarón el proyecto.

Por último creamos un objeto de la clase aplicación.
~~~py
aplicacion1=aplicacion()
~~~


# **Código Fuente**

~~~py
'''
@Roberto Ramírez <rramirezg18@miumg.edu.gt
@Editor de texto con interfaz gráfica Tkinter
@date 02/11/2022
@license GNU General Public License v. 1.0
'''
import tkinter as tk
from tkinter import scrolledtext as st
from tkinter import filedialog as fd
from tkinter import messagebox as mb
import os

class aplicacion:
    def __init__(self):
        self.app=tk.Tk()
        self.app.title("Editor de texto - Proyecto 3")
        self.menu()
        self.texto=st.ScrolledText(self.app, width=70, height=20, undo=True, font=("Comic Sans MS", 12) )
        self.texto.grid(padx=5, pady=3)      
        self.app.mainloop()

    def menu(self):
        barramenu = tk.Menu(self.app)
        self.app.config(menu=barramenu)
        menuarchivo = tk.Menu(barramenu, tearoff=0)
        menueditar = tk.Menu(barramenu, tearoff=0)
        menuayuda = tk.Menu(barramenu, tearoff=0)
        menuarchivo.add_command(label="Nuevo", command=self.nuevo)
        menuarchivo.add_command(label="Abir", command=self.abrir)
        menuarchivo.add_command(label="Guardar", command=self.guardar)
        menuarchivo.add_command(label="Guardar como", command=self.guardarcomo)
        menuarchivo.add_separator()
        menuarchivo.add_command(label="Salir", command=self.app.destroy)
        barramenu.add_cascade(label="Archivo", menu=menuarchivo)
        #menueditar.add_command(label="Deshacer", command=self.deshacer)
        #menueditar.add_command(label="Rehacer", command=self.rehacer)
        menueditar.add_command(label="Deshacer")#, command=self.texto.edit_undo
        menueditar.add_command(label="Rehacer")#, command=self.texto.edit_redo
        menueditar.add_separator()
        menueditar.add_command(label="Borrar Todo", command=self.borrar)
        barramenu.add_cascade(label="Editar", menu=menueditar)
        menuayuda.add_command(label="Información", command=self.licencia)
        menuayuda.add_command(label="Manual de usuario", command=self.manual)
        menuayuda.add_command(label="Integrantes", command=self.integrantes)
        barramenu.add_cascade(label="Ayuda", menu=menuayuda)

    def deshacer(self, event=None):
        self.app.event_generate("<<undo>>")
        
    def rehacer(self, event=None):
        self.app.event_generate("<<redo>>")

    def borrar(self):
        self.texto.delete("1.0", tk.END)

    def guardarcomo(self): 
        nombrearchivo=fd.asksaveasfilename(initialdir = "/",title = "Guardar como",filetypes = (("txt files","*.txt"),("todos los archivos","*.*")))
        if nombrearchivo!='':
            archivo=open(nombrearchivo, "w", encoding="utf-8")
            archivo.write(self.texto.get("1.0", tk.END))
            archivo.close()
            mb.showinfo("Información", "Archivo guardado correctamente")
            
    def guardar(self):
        nombrearchivo=fd.asksaveasfilename(initialdir = "/",title = "Guardar",filetypes = (("txt files","*.txt"),("todos los archivos","*.*")))
        if nombrearchivo!='':
            archivo=open(nombrearchivo, "w", encoding="utf-8")
            archivo.write(self.texto.get("1.0", tk.END))
            archivo.close()
            mb.showinfo("Información", "Los datos fueron guardados en el archivo.")

    def abrir(self):
        nombrearchivo=fd.askopenfilename(initialdir = "/",title = "Seleccione archivo",filetypes = (("txt files","*.txt"),("todos los archivos","*.*")))
        if nombrearchivo!='':
            archivo=open(nombrearchivo, "r", encoding="utf-8")
            contenido=archivo.read()
            archivo.close()
            self.texto.delete("1.0", tk.END) 
            self.texto.insert("1.0", contenido)
    def nuevo(self):
        self.texto.delete("1.0", tk.END)
            
    def manual(self):
        os.startfile(".\doc\Tarea.pdf")

    def licencia(self):
        mb.showinfo("Licencia", "GNU General Public License v. 1.0\nEditor de texto con interfaz grafica Tkinter\nPython 3.10.4")

    def integrantes(self):
        os.startfile(".\doc\Integrantes.txt")

aplicacion1=aplicacion()
~~~
