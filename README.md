# -EcoCityManager
Sistema de Gestão de Recolha de Lixo desenvolvido em c++
Este projeto é um sistema desenvolvido em C++ para a gestão de recolha de lixo urbano. O sistema permite registar e organizar informações sobre zonas da cidade, camiões, motoristas e rotas de recolha.

Através de um menu interativo, o utilizador pode:

* Adicionar e listar zonas da cidade
* Registar camiões e associá-los a zonas específicas
* Registar motoristas
* Criar e visualizar rotas de recolha
* Consultar estatísticas gerais do sistema

O objetivo do projeto é simular a organização eficiente de serviços de limpeza urbana, facilitando o controlo de recursos e operações.

#include <iostream>
#include <vector>
#include <fstream>
#include <string>
#include <limits>

using namespace std;

// ================= ESTRUTURAS =================
struct Zona {
    int id;
    string nome;
};

struct Camiao {
    int id;
    string matricula;
    int zonaId; // nova ligação
};

struct Motorista {
    int id;
    string nome;
};

struct Rota {
    int camiaoId;
    int zonaId;
};

// ================= DADOS =================
vector<Zona> zonas;
vector<Camiao> camioes;
vector<Motorista> motoristas;
vector<Rota> rotas;

// ================= UTIL =================
void limparBuffer() {
    cin.ignore(numeric_limits<streamsize>::max(), '\n');
}

// ================= ZONAS =================
void adicionarZona() {
    Zona z;
    z.id = zonas.size() + 1;

    cout << "Nome da zona: ";
    limparBuffer();
    getline(cin, z.nome);

    zonas.push_back(z);
}

void listarZonas() {
    cout << "\n--- ZONAS ---\n";
    for (auto &z : zonas)
        cout << z.id << " - " << z.nome << endl;
}

// ================= CAMIOES =================
void adicionarCamiao() {
    Camiao c;
    c.id = camioes.size() + 1;

    cout << "Matricula: ";
    cin >> c.matricula;

    cout << "ID da zona atribuida: ";
    cin >> c.zonaId;

    camioes.push_back(c);
}

void listarCamioes() {
    cout << "\n--- CAMIOES ---\n";
    for (auto &c : camioes) {
        cout << c.id << " - " << c.matricula;

        for (auto &z : zonas) {
            if (z.id == c.zonaId) {
                cout << " (Zona: " << z.nome << ")";
            }
        }
        cout << endl;
    }
}

// ================= MOTORISTAS =================
void adicionarMotorista() {
    Motorista m;
    m.id = motoristas.size() + 1;

    cout << "Nome: ";
    limparBuffer();
    getline(cin, m.nome);

    motoristas.push_back(m);
}

void listarMotoristas() {
    cout << "\n--- MOTORISTAS ---\n";
    for (auto &m : motoristas)
        cout << m.id << " - " << m.nome << endl;
}

// ================= ROTAS =================
void criarRota() {
    Rota r;

    cout << "ID camiao: ";
    cin >> r.camiaoId;

    cout << "ID zona: ";
    cin >> r.zonaId;

    rotas.push_back(r);
}

void listarRotas() {
    cout << "\n--- ROTAS ---\n";

    for (auto &r : rotas) {
        cout << "Camiao " << r.camiaoId << " -> Zona " << r.zonaId << endl;
    }
}

// ================= ESTATISTICAS =================
void estatisticas() {
    cout << "\n--- ESTATISTICAS ---\n";
    cout << "Total zonas: " << zonas.size() << endl;
    cout << "Total camioes: " << camioes.size() << endl;
    cout << "Total motoristas: " << motoristas.size() << endl;
    cout << "Total rotas: " << rotas.size() << endl;
}

// ================= MENU =================
int main() {
    int op;

    do {
        cout << "\n===== ECO CITY MANAGER =====\n";
        cout << "1. Adicionar Zona\n";
        cout << "2. Listar Zonas\n";
        cout << "3. Adicionar Camiao\n";
        cout << "4. Listar Camioes\n";
        cout << "5. Adicionar Motorista\n";
        cout << "6. Listar Motoristas\n";
        cout << "7. Criar Rota\n";
        cout << "8. Listar Rotas\n";
        cout << "9. Estatisticas\n";
        cout << "0. Sair\n";
        cout << "Opcao: ";
        cin >> op;

        switch (op) {
            case 1: adicionarZona(); break;
            case 2: listarZonas(); break;
            case 3: adicionarCamiao(); break;
            case 4: listarCamioes(); break;
            case 5: adicionarMotorista(); break;
            case 6: listarMotoristas(); break;
            case 7: criarRota(); break;
            case 8: listarRotas(); break;
            case 9: estatisticas(); break;
        }

    } while (op != 0);

    return 0;
}