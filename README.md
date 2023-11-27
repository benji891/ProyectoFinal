# ProyectoFinal
Proyecto Final
[17:21, 19/11/2023] +51 959 539 594: #include<iostream>
#include<conio.h>
#include<string>
#include<vector>
#include<cstdlib>
#include<windows.h>
#define color SetConsoleTextAttribute
using namespace std;
HANDLE hConsole = GetStdHandle(STD_OUTPUT_HANDLE);

struct Usuario
{
	string nombre;
	string contrasena;
	int codigo, tipo; 
};
struct Producto
{
	int codigo;
	int stock;
	string nombre;
	float precio;
};
struct Cliente
{
	string nombre;
	int DNI, codigo;
};
struct ProductosVendidos
{
	string producto;
	int cantidadextraida;
	int posicion;
	int venta;
};
struct Venta
{
	int numero;
	float importepago;
	string nombreCliente;
	string nombreVendedor;
};
vector <Usuario> VecUsuario;
vector <Producto> vecProducto;
vector <Cliente> vecCliente;
vector <ProductosVendidos> vecProVenta;
vector <Venta> v…
[17:21, 19/11/2023] +51 959 539 594: zinjai
[18:08, 19/11/2023] Tona Usil: #include<iostream>
#include<conio.h>
#include<string>
#include<vector>
using namespace std;
using namespace System;
struct Usuario
{
	string nombre;
	string contraseña;
	int codigo, tipo; //1: Administrador; 2: Vendedor
};
struct Producto
{
	int codigo;
	int stock;
	string nombre;
	float precio;
};
struct Cliente
{
	string nombre;
	int DNI, codigo;
};
struct ProductosVendidos
{
	string producto;
	int cantidadextraida;
	int posicion;
	int venta;
};
struct Venta
{
	int numero;
	float importepago;
	string nombreCliente;
	string nombreVendedor;
};
vector <Usuario> VecUsuario;
vector <Producto> vecProducto;
vector <Cliente> vecCliente;
vector <ProductosVendidos> vecProVenta;
vector <Venta> vecVenta;
/PROTOTIPOS/
void Add_Data();
void Iniciar_Sesion();
int Get_Correlativo();
void Registro_Productos();
int Get_CorrelativoCliente();
void Registro_Clientes();
void Menu_Admin();
void Menu_Vendedor();
void Registro_Vendedores();
int Get_NumeroVenta();
void Generar_Venta();
void Anular_Ventas();
void Listar_Ventas();
void Listar_Productos();
int main()
{
	int eleccion;
	Add_Data();
	do {
		Console::Clear();
		Console::ForegroundColor = ConsoleColor::Green;
		cout << "\t\t\t\t\t\tBIENVENIDO A VENTAMAS\n\n";
		Console::ForegroundColor = ConsoleColor::Cyan; setlocale(LC_ALL, "");
		cout << "\t\t\t\t1) Iniciar sesión.\n";
		cout << "\t\t\t\t2) Salir.\n";
		setlocale(LC_ALL, ""); cout << "\t\t\t\t¿Qué desea hacer? "; cin >> eleccion;
		switch (eleccion)
		{
		case 1: Iniciar_Sesion(); break;
		case 2: cout << "\t\t\t\tHasta luego!"; _sleep(500); break;
		default:;
		}
	} while (eleccion != 2);
}
/IMPLEMENTACION/
void Add_Data()
{
	Usuario default1;
	default1.codigo = 1;
	default1.nombre = "Tomas Davila";
	default1.contraseña = "TONADAV123";
	default1.tipo = 1;
	VecUsuario.push_back(default1);
	Usuario default2;
	default2.codigo = 2;
	default2.nombre = "Benjamin Ramirez";
	default2.contraseña = "HOLAMUNDO";
	default2.tipo = 1;
	VecUsuario.push_back(default2);
	Usuario default3;
	default3.codigo = 3;
	default3.nombre = "Diego Garcia";
	default3.contraseña = "AQUI";
	default3.tipo = 2;
	VecUsuario.push_back(default3);
	Usuario default4;
	default4.codigo = 4;
	default4.nombre = "Edison Flores";
	default4.contraseña = "UNIVERSITARIO";
	default4.tipo = 2;
	VecUsuario.push_back(default4);
	Usuario default5;
	default5.codigo = 5;
	default5.nombre = "Matias Marengo";
	default5.contraseña = "ALIANZA";
	default5.tipo = 2;
	VecUsuario.push_back(default5);

	Producto primero;
	primero.codigo = 1;
	primero.nombre = "Lapiz";
	primero.precio = 2.50;
	primero.stock = 15;
	vecProducto.push_back(primero);
	Producto segundo;
	segundo.codigo = 2;
	segundo.nombre = "Lapicero";
	segundo.precio = 3.50;
	segundo.stock = 15;
	vecProducto.push_back(segundo);
	Producto tercero;
	tercero.codigo = 3;
	tercero.nombre = "Borrador";
	tercero.precio = 1.50;
	tercero.stock = 10;
	vecProducto.push_back(tercero);

	Cliente primeroo;
	primeroo.nombre = "Fernando Velasco";
	primeroo.DNI = 34561245;
	primeroo.codigo = 1;
	vecCliente.push_back(primeroo);
}
void Iniciar_Sesion()
{
	string   nombre, contraseña, identidad;
	char     caracter;
	int      intentos = 0, tipo;
	bool     estado = false;
	do {
		Console::Clear();
		Console::ForegroundColor = ConsoleColor::Green;
		setlocale(LC_ALL, ""); cout << "\t\t\t\t\t\tINICIO DE SESIÓN\n\n";
		Console::ForegroundColor = ConsoleColor::Cyan; 
		cin.ignore();
		cout << "\t\t\t\tIngrese su nombre completo: "; getline(cin, nombre);
		setlocale(LC_ALL, ""); cout << "\n\t\t\t\tIngrese su contraseña: ";
		caracter = getch();
		contraseña = "";
		while (caracter != 13)
		{
			if (caracter != 8)
			{
				contraseña.push_back(caracter);
				cout << "*";
			}
			else
			{
				if (contraseña.length() > 0)
				{
					cout << "\b \b";
					contraseña = contraseña.substr(0, contraseña.length() - 1);
				}
			}
			caracter = getch();
		}
		for (int i = 0; i < VecUsuario.size(); i++)
		{
			if (nombre == VecUsuario[i].nombre && contraseña == VecUsuario[i].contraseña)
			{
				estado = true;
				tipo = VecUsuario[i].tipo;
				identidad = VecUsuario[i].nombre;
			}
		}
		if (!estado)
		{
			intentos++;
		}
	} while (estado == false && intentos < 3);
	if (estado == false)
	{
		setlocale(LC_ALL, ""); cout << "\n\t\t\t\tAcceso denegado. Adiós.\n"; _getch();
	}
	else
	{
		switch (tipo)
		{
		case 1: cout << "\n\n\t\t\t\tBienvenido señor  " << identidad; _sleep(1500); Menu_Admin(); break;
		case 2: cout << "\n\n\t\t\t\tBienvenido!"; _sleep(1500); Menu_Vendedor();
		}
	}
}
int Get_Correlativo()
{
	if (vecProducto.size() == 0)
		return 1;
	else
		return vecProducto[vecProducto.size() - 1].codigo + 1;
}
void Registro_Productos()
{
	Producto data;
	string nombre;
	int codigo;
	float precio;
	int stock;
	char respuesta;
	do {
		Console::Clear();
		Console::ForegroundColor = ConsoleColor::Green;
		cout << "\t\t\t\t\t\tREGISTRO DE PRODUCTOS\n\n";
		Console::ForegroundColor = ConsoleColor::Cyan;
		setlocale(LC_ALL, ""); cout << "\t\t\t\tCódigo: " << Get_Correlativo() << endl;
		data.codigo = Get_Correlativo();
		cin.ignore();
		Console::ForegroundColor = ConsoleColor::Cyan;
		cout << "\t\t\t\tIngrese nombre del producto: "; getline(cin, nombre);
		data.nombre = nombre; 
		cout << "\t\t\t\tIngrese precio: "; cin >> precio;
		data.precio = precio;
		cout << "\t\t\t\tIngrese stock: "; cin >> stock;
		data.stock = stock;
		vecProducto.push_back(data);
		cout << "\t\t\t\tDesea continuar? "; cin >> respuesta;
	} while (respuesta == 'S' || respuesta == 's');
}
int Get_CorrelativoCliente()
{
	if (vecCliente.size() == 0)
		return 1;
	else
		return vecCliente[vecCliente.size() - 1].codigo + 1;
}
void Registro_Clientes()
{
	Cliente registro;
	string nombre;
	int DNI;
	Console::Clear();
	Console::ForegroundColor = ConsoleColor::Green;
	cout << "\t\t\t\t\t\tREGISTRO DE CLIENTES\n";
	Console::ForegroundColor = ConsoleColor::Cyan;
	setlocale(LC_ALL, ""); cout << "\t\t\t\tCódigo: " << Get_CorrelativoCliente() << endl;;
	registro.codigo = Get_CorrelativoCliente();
	cin.ignore();
	cout << "\t\t\t\tIngrese nombre: "; getline(cin, nombre);
	registro.nombre = nombre;
	do {
		Console::ForegroundColor = ConsoleColor::Cyan;
		cout << "\t\t\t\tIngrese DNI: "; cin >> DNI;
	} while (DNI < 10000000 || DNI>99999999);
	registro.DNI = DNI;
	vecCliente.push_back(registro);
	Console::ForegroundColor = ConsoleColor::White;
	cout << "\t\t\t\tCliente registrado exitosamente!";
}
void Registro_Vendedores()
{
	Usuario input;
	string nombre;
	char respuesta;
	int tipo=2;
	do {
		Console::Clear();
		Console::ForegroundColor = ConsoleColor::Green;
		cout << "\t\t\t\t\t\tREGISTRO DE VENDEDORES\n\n";
		cin.ignore();
		Console::ForegroundColor = ConsoleColor::Cyan;
		input.tipo = tipo;
		cout << "\t\t\t\tIngrese nombre: "; getline(cin, nombre);
		input.nombre = nombre;
		VecUsuario.push_back(input);
		Console::ForegroundColor = ConsoleColor::White;
		cout << "\t\t\t\t\nDesea continuar? "; cin >> respuesta;
	} while (respuesta == 's' || respuesta == 'S');
}
int Get_NumeroVenta()
{
	if (vecVenta.size() == 0)
		return 1;
	else
		return vecVenta[vecVenta.size() - 1].numero + 1;
}
void Generar_Venta()
{
	Venta generar;
	ProductosVendidos generate;
	string nombreCliente;
	string nombreProducto;
	string nombreVendedor;
	bool estado = false, state = false, estadoo = false;
	float suma = 0;
	char rpta;
	int numeroventa;
	Console::ForegroundColor = ConsoleColor::Cyan;
	generar.numero = Get_NumeroVenta();
	numeroventa= Get_NumeroVenta();
	do {
		Console::Clear();
		Console::ForegroundColor = ConsoleColor::Green;
		setlocale(LC_ALL, ""); cout << "\t\t\t\t\t\tGENERACIÓN DE VENTA\n\n";
		cin.ignore();
		Console::ForegroundColor = ConsoleColor::Cyan;
		setlocale(LC_ALL, ""); cout << "\t\t\t\tNúmero de venta: " << Get_NumeroVenta()<<endl;
		cout << "\t\t\t\tIngrese nombre del vendedor: "; getline(cin, nombreVendedor);
		for (int i = 0; i < VecUsuario.size(); i++)
		{
			if (nombreVendedor== VecUsuario[i].nombre)
			{
				generar.nombreVendedor = VecUsuario[i].nombre;
				estadoo = true;
				break;
			}
		}
	} while (estadoo == false);
	do {
		cin.ignore();
		Console::ForegroundColor = ConsoleColor::Cyan;
		cout << "\n\t\t\t\tIngrese nombre del cliente: "; getline(cin, nombreCliente);
		for (int i = 0; i < vecCliente.size(); i++)
		{
			if (nombreCliente==vecCliente[i].nombre )
			{
				generar.nombreCliente = vecCliente[i].nombre;
				estado = true;
				break;
			}
		}
	} while (estado == false);
	do {
		cin.ignore();
		Console::ForegroundColor = ConsoleColor::Cyan;
		cout << "\n\t\t\t\tIngrese nombre del producto: "; getline(cin, nombreProducto);
		for (int i = 0; i < vecProducto.size(); i++)
		{
			if (nombreProducto==vecProducto[i].nombre)
			{
				state = true;
				int cantidad = 0;
				Console::ForegroundColor = ConsoleColor::White;
				cout << "\t\t\t\tIngrese cantidad a comprar: "; cin >> cantidad; 
				vecProducto[i].stock -= cantidad; 
				if (vecProducto[i].stock < 0)
				{
					Console::ForegroundColor = ConsoleColor::White;
					cout << "\t\t\t\tSTOCK AGOTADO!" << endl; 
					vecProducto[i].stock += cantidad;
				}
				else
				{
					suma += vecProducto[i].precio * cantidad;
					generar.importepago = suma;
					generate.producto = vecProducto[i].nombre;
					generate.cantidadextraida = cantidad;
					generate.posicion = vecProducto[i].codigo;
					generate.venta = numeroventa;
					vecProVenta.push_back(generate);
				}
				break;
			}
		}
		Console::ForegroundColor = ConsoleColor::White;
		cout << "\t\t\t\tDesea adquirir otro producto? "; cin >> rpta;
	} while (rpta == 's' || rpta == 'S');
	Console::ForegroundColor = ConsoleColor::White;
	cout << "\t\t\t\tImporte a pagar: s/." << suma << endl;
	vecVenta.push_back(generar);
}
void Anular_Ventas()
{
	int numero, cantidad;
	bool bandera = false;
	string nombre;
	Console::Clear();
	Console::ForegroundColor = ConsoleColor::Green;
	setlocale(LC_ALL, ""); cout << "\t\t\t\t\t\tANULACIÓN DE VENTA\n";
	Console::ForegroundColor = ConsoleColor::Cyan;
	setlocale(LC_ALL, ""); cout << "\t\t\t\tIngrese número de venta a eliminar: "; cin >> numero;
	for (int i = 0; i < vecVenta.size(); i++)
	{
		if (numero == vecVenta[i].numero)
		{
			bandera = true;
			for (int j = 0; j < vecProVenta.size(); j++)
			{
				if (numero == vecProVenta[j].venta)
				{
					nombre = vecProVenta[j].producto;
					cantidad = vecProVenta[j].cantidadextraida;
					for (int k = 0; k < vecProducto.size(); k++)
					{
						if (nombre == vecProducto[k].nombre)
						{
							vecProducto[k].stock += cantidad;
						}
					}
					//vecProVenta.erase(vecProVenta.begin() + j);
				}
			}
			vecVenta.erase(vecVenta.begin() + i);
		}
	}
	if (bandera == true)
	{
		Console::ForegroundColor = ConsoleColor::White;
		cout << "\t\t\t\tVenta anulada exitosamente!" << endl;
	}
	else
	{
		Console::ForegroundColor = ConsoleColor::White;
		setlocale(LC_ALL, ""); cout << "\t\t\t\tEl número de venta no existe!" << endl;
	}
}
void Menu_Admin()
{
	int opcion;
	do {
		Console::Clear();
		Console::ForegroundColor = ConsoleColor::Green; setlocale(LC_ALL, "");
		cout << "\t\t\t\t\t\tMENÚ DEL ADMINISTRADOR\n\n";
		Console::ForegroundColor = ConsoleColor::Cyan;
		cout << "\t\t\t\t1) REGISTRO DE CLIENTES\n";
		cout << "\t\t\t\t2) REGISTRO DE PRODUCTOS\n";
		cout << "\t\t\t\t3) REGISTRO DE VENDEDORES\n";
		cout << "\t\t\t\t4) LISTA DE VENTAS\n";
		cout << "\t\t\t\t5) LISTA DE PRODUCTOS\n";
		cout << "\t\t\t\t6) SALIR\n";
		Console::ForegroundColor = ConsoleColor::White;
		setlocale(LC_ALL, ""); cout << "\t\t\t\tSeleccione una opción: "; cin >> opcion;
		switch (opcion)
		{
		case 1: Registro_Clientes(); _getch(); break;
		case 2: Registro_Productos(); _getch(); break;
		case 3: Registro_Vendedores(); _getch(); break;
		case 4: Listar_Ventas(); _getch(); break;
		case 5: Listar_Productos(); _getch(); break;
		case 6: ; break;
		default: setlocale(LC_ALL, ""); cout << "\t\t\t\tIngrese una opción correcta (1-6). Presione cualquier tecla para continuar "; _getch();
		}
	} while (opcion != 6);
}
void Menu_Vendedor()
{
	int opcion;
	do {
		Console::Clear(); 
		Console::ForegroundColor = ConsoleColor::Green; setlocale(LC_ALL, "");
		cout << "\t\t\t\t\t\tMENÚ DEL VENDEDOR\n\n";
		Console::ForegroundColor = ConsoleColor::Cyan;
		cout << "\t\t\t\t1) GENERAR VENTA\n";
		cout << "\t\t\t\t2) ANULAR VENTA\n";
		cout << "\t\t\t\t3) LISTA DE PRODUCTOS\n";
		cout << "\t\t\t\t4) SALIR\n";
		Console::ForegroundColor = ConsoleColor::White;
		setlocale(LC_ALL, ""); cout << "\t\t\t\tSeleccione una opción: ";
		cin >> opcion;
		switch (opcion)
		{
		case 1: Generar_Venta(); _getch(); break;
		case 2: Anular_Ventas();  _getch(); break;
		case 3: Listar_Productos(); _getch(); break;
		case 4: ; break;
		default: setlocale(LC_ALL, ""); cout << "\t\t\t\tIngrese una opción correcta (1-4). Presione cualquier tecla para continuar "; _getch();
		}
	} while (opcion != 4);
}
void Listar_Ventas()
{
	Console::Clear();
	Console::ForegroundColor = ConsoleColor::Green;
	int numero;
	cout << "\t\t\t\t\t\tLISTA DE VENTAS\n\n";
	if (vecVenta.size() == 0)
	{
		Console::ForegroundColor = ConsoleColor::Cyan;
		cout << "\t\t\t\tNo hay ventas registradas!";
	}
	else
	{
		for (int i = 0; i < vecVenta.size(); i++)
		{
			Console::ForegroundColor = ConsoleColor::Cyan;
			cout << "\n\t\t\t\t-------------------------------------------" << endl;
			setlocale(LC_ALL, ""); cout << "\t\t\t\tNúmero de venta: " << vecVenta[i].numero << endl;
			cout << "\t\t\t\tNombre del vendedor: " << vecVenta[i].nombreVendedor << endl;
			cout << "\t\t\t\tNombre del cliente: " << vecVenta[i].nombreCliente << endl;
			cout << "\t\t\t\tProducto(s) adquirido(s): \n";
			numero = vecVenta[i].numero;
			for (int i = 0; i < vecProVenta.size(); i++)
			{
				if (numero == vecProVenta[i].venta)
				{
					cout << "\t\t\t\t" << vecProVenta[i].producto << endl;
				}
			}
			cout << "\t\t\t\tImporte pagado: s/" << vecVenta[i].importepago << endl;
		}
	}
}
void Listar_Productos()
{
	Console::Clear();
	Console::ForegroundColor = ConsoleColor::Green;
	cout << "\t\t\t\t\t\tLISTA DE PRODUCTOS\n\n";
	for (int i = 0; i < vecProducto.size(); i++)
	{
		Console::ForegroundColor = ConsoleColor::Cyan;
		cout << "\t\t\t\tProducto: " << vecProducto[i].nombre << " | " << "Stock: " << vecProducto[i].stock << endl;
	}
}
