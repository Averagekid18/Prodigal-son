# The prodigal son
//Proyecto programacion estructurada

#include <stdlib.h>
#include <iostream>
#include <fstream>
using namespace std;

const int MAX_SALARIOS = 2;
string entreContra, pass2;


//**************************************************************************//
//recuperado desde chatgpt//

void funcUtil(int gastos[], int index) {
    int comida, Utilidades, Ext;
    cout << "Cuanto paga total de utilidades mensual (Agua, Luz, carro): ";
    cin >> Utilidades;
    gastos[index] += Utilidades;
    cout << "Cuanto paga en comida mensual: ";
    cin >> comida;
    gastos[index] += comida;
    cout << "Cuanto paga mensual en cosas miscelaneas: ";
    cin >> Ext;
    cout << "**************************************************************************** \n";
    gastos[index] += Ext;

}
//****************************************************************************//

int funcCasado(int sal[], int Sumsal) {
    int gastos[MAX_SALARIOS] = { 0 };
    int totalC = 0;
    for (int i = 0; i < Sumsal; i++) {
        totalC += sal[i];
    }
    cout << "La suma de sus salarios entrados son: " << totalC << endl;

    char opcion;

    do {
        cout << "**************************************************************************** \n";
        cout << "Usted tiene una casa o apartamento? Entre C para casa, o A para apartamento: ";
        cin >> opcion;
        cout << "**************************************************************************** \n";

        if (opcion == 'C' || opcion == 'c') {
            cout << "Cuanto paga mensual en su casa ";
            cin >> sal[0];
            funcUtil(gastos, 0);
        }

        else if (opcion == 'A' || opcion == 'a') {
            cout << "Cuanto paga mensual en su apartamento? ";
            cin >> sal[1];
            funcUtil(gastos, 1);
        }
        else {
            cout << "Input no reconocido\n";
            system("cls");
        }
    } while (opcion != 'C' && opcion != 'c' && opcion != 'A' && opcion != 'a');

    int gastosTotales = gastos[0] + gastos[1];
    int dineroRestante = totalC - gastosTotales;
    cout << "Esto lo dejaria con " << dineroRestante << "$ para usar mensualmente \n";

    return dineroRestante;
}

int funcSoltero(int salM) {
    int gastos[MAX_SALARIOS] = { 0 };
    char opcion;
    do {
        cout << "Usted tiene una casa o apartamento? Entre C para casa, o A para apartamento: ";
        cin >> opcion;
        cout << "**************************************************************************** \n";

        if (opcion == 'C' || opcion == 'c' || opcion == 'A' || opcion == 'a') {
            int costo;
            cout << "Cuanto paga mensualmente por su vivienda: ";
            cin >> costo;
            funcUtil(gastos, 0);
            gastos[0] += costo;
        }
        else {
            cout << "Input no reconocido\n";
            system("cls");
        }
    } while (opcion != 'C' && opcion != 'c' && opcion != 'A' && opcion != 'a');

    int gastosTotales = gastos[0];
    int dineroRestante = salM - gastosTotales;
    cout << "Esto lo dejaria con " << dineroRestante << "$ para usar mensualmente \n";
    return dineroRestante;
}

int main() {
    int opcion, salM, sal[MAX_SALARIOS];
    string password, pass2, entreContra;

    ofstream info;

    do {
        cout << "********************************************** \n";
        cout << "Bienvenidos a tu propio manejador de finanzas: \n";
        cout << "********************************************** \n";
        cout << "Para proteger su cuenta, cree un password: \n";
        cout << "(No use espacios cuando cree el password) \n";
        cin >> password;
        cout << "Confirme el password creado: \n";
        cin >> pass2;
        system("cls");

    } while (password != pass2);

    cout << "********************************************** \n";
    cout << "Si estas casado oprima 1 \n";
    cout << "Si esta soltero oprima 2 \n";
    cout << "Si deseas salir oprima 3 \n";
    cout << "********************************************** \n";
    cin >> opcion;
    system("cls"); // Borra la pantalla

    if (opcion == 1) {
        cout << "******************************* \n";
        cout << "Favor entrar el primer salario mensual: \n";
        cin >> sal[0];
        cout << "******************************* \n";
        cout << "Ahora el segundo salario mensual: \n";
        cin >> sal[1];
        cout << "******************************* \n";
        int dinerorestante = funcCasado(sal, MAX_SALARIOS);
        cout << "******************************* \n";
        do {
            cout << "Comprovemos su contraseña para poder ver su informacion: \n";
            cout << "Entre su contraseña: ";
            cin >> entreContra;
            if (entreContra == pass2) {

                cout << "Su informacion sera guardada en un archivo.\n";
                cout << "Lo puede buscar como 'info.txt' en el search de archivos\n";
                cout << "Gracias por usar la calculadora de finansas, haga clic en cuarquier tecla para salir del programa.";
                cout << "";
                info.open("infor.txt");
                info << "Su contraceña es: " << pass2 << endl;
                info << "Su total restante es de " << dinerorestante << endl;
                info << "Algunas recomendaciones que le aconcejamos para pueda ahorrar mucho mas dinero son: \n";
                info << "Elaborar un presupuesto, toma buenas deciciones economicamente, crear una cuenta de ahorros, ten diciplina para no malgastar, ext.\n";

                info.close();
            }
            else {
                cout << "Contraceña denegada\n";
            }
        } while (entreContra != pass2);

    }
    if (opcion == 2) {
        cout << "******************************** \n";
        cout << "Favor entrar su salario mensual: \n";
        cin >> salM;
        cout << "******************************** \n";
        int dinerorestante = funcSoltero(salM);
        cout << "******************************* \n";
        do {
            cout << "Comprovemos su contraseña para poder ver su informacion: \n";
            cout << "Entre su contraseña: ";
            cin >> entreContra;
            if (entreContra == pass2) {
                cout << "Su informacion sera guardada en un archivo\n";
                cout << "Lo puede buscar como 'info.txt' en el search de archivos\n";
                cout << "Gracias por usar la calculadora de finansas, haga clic en cuarquier tecla para salir del programa.";
                cout << "";
                info.open("infor.txt");
                info << "Su contraceña es: " << pass2 << endl;
                info << "Su total restante es de " << dinerorestante << endl;
                info << "Algunas recomendaciones que le aconcejamos para pueda ahorrar mucho mas dinero son: \n";
                info << "Elaborar un presupuesto, toma buenas deciciones economicamente, crear una cuenta de ahorros, ten diciplina para no malgastar, ext.\n";
                info.close();
            }
            else {
                cout << "Contraceña denegada\n";
            }
        } while (entreContra != pass2);

    }
    if (opcion == 3) {
        cout << "Que tenga buen dia, adios";
        //se acaba el programa
    }
    return 0;
}
