package main

import (
	"fmt"
)

type Estudiante struct {
	Nombre  string
	ID      int
	Carrera string
}

var registroEstudiantes []Estudiante

func AgregarEstudiante(slice []Estudiante, estudiante Estudiante) []Estudiante {
	return append(slice, estudiante)
}

func BuscarEstudiantePorID(slice []Estudiante, id int) *Estudiante {
	for i := range slice {
		if slice[i].ID == id {
			return &slice[i]
		}
	}
	return nil
}

func ActualizarEstudiantePorID(slice []Estudiante, id int, nuevoNombre string, nuevaCarrera string) bool {
	for i := range slice {
		if slice[i].ID == id {
			slice[i].Nombre = nuevoNombre
			slice[i].Carrera = nuevaCarrera
			return true
		}
	}
	return false
}

func EliminarEstudiantePorID(slice []Estudiante, id int) []Estudiante {
	for i := range slice {
		if slice[i].ID == id {
			return append(slice[:i], slice[i+1:]...)
		}
	}
	return slice
}

func ListarEstudiantes(slice []Estudiante) {
	if len(slice) == 0 {
		fmt.Println("No hay estudiantes registrados.")
		return
	}
	for _, estudiante := range slice {
		fmt.Printf("Nombre: %s, ID: %d, Carrera: %s\n", estudiante.Nombre, estudiante.ID, estudiante.Carrera)
	}
}

func main() {
	for {
		fmt.Println("Menú:")
		fmt.Println("1. Agregar estudiante")
		fmt.Println("2. Buscar estudiante por ID")
		fmt.Println("3. Listar estudiantes")
		fmt.Println("4. Actualizar estudiante por ID")
		fmt.Println("5. Eliminar estudiante por ID")
		fmt.Println("6. Salir")
		fmt.Print("Seleccione una opción: ")

		var opcion int
		fmt.Scan(&opcion)

		switch opcion {
		case 1:
			var nombre, carrera string
			var id int
			fmt.Print("Ingrese nombre: ")
			fmt.Scan(&nombre)
			fmt.Print("Ingrese ID: ")
			fmt.Scan(&id)
			fmt.Print("Ingrese carrera: ")
			fmt.Scan(&carrera)
			registroEstudiantes = AgregarEstudiante(registroEstudiantes, Estudiante{Nombre: nombre, ID: id, Carrera: carrera})
			fmt.Println("Estudiante agregado correctamente.")
		case 2:
			var id int
			fmt.Print("Ingrese el ID del estudiante a buscar: ")
			fmt.Scan(&id)
			estudiante := BuscarEstudiantePorID(registroEstudiantes, id)
			if estudiante != nil {
				fmt.Printf("Estudiante encontrado - Nombre: %s, ID: %d, Carrera: %s\n", estudiante.Nombre, estudiante.ID, estudiante.Carrera)
			} else {
				fmt.Println("Estudiante no encontrado.")
			}
		case 3:
			ListarEstudiantes(registroEstudiantes)
		case 4:
			var id int
			var nuevoNombre, nuevaCarrera string
			fmt.Print("Ingrese el ID del estudiante a actualizar: ")
			fmt.Scan(&id)
			fmt.Print("Ingrese el nuevo nombre: ")
			fmt.Scan(&nuevoNombre)
			fmt.Print("Ingrese la nueva carrera: ")
			fmt.Scan(&nuevaCarrera)
			if ActualizarEstudiantePorID(registroEstudiantes, id, nuevoNombre, nuevaCarrera) {
				fmt.Println("Estudiante actualizado correctamente.")
			} else {
				fmt.Println("Estudiante no encontrado.")
			}
		case 5:
			var id int
			fmt.Print("Ingrese el ID del estudiante a eliminar: ")
			fmt.Scan(&id)
			registroEstudiantes = EliminarEstudiantePorID(registroEstudiantes, id)
			fmt.Println("Estudiante eliminado correctamente.")
		case 6:
			fmt.Println("Saliendo del programa.")
			return
		default:
			fmt.Println("Opción no válida, intente de nuevo.")
		}
	}
}