#include <iostream>
#include <vector>

using namespace std;

struct usuario{
string nome;
string senha;
string funcao;

};
vector<usuario> contas;
vector<usuario>:: iterator it;


int login(){
usuario a{"admin","admin","operador"};
contas.push_back(a);
int flag = 0;


    cout<<"_________LOGIN_________"<<endl;
    usuario acess;
    cout<<"Digite o nome de usuario: ";
    cin>>acess.nome;

    for(it = contas.begin(); it!= contas.end(); ++it){
        if(it->nome == acess.nome){
                cout<<"o nome esta : "<<it->nome<<endl;
            cout<<"por favor digite a senha: ";
            cin>>acess.senha;
            for(it = contas.begin(); it!= contas.end(); ++it){
                if(it->senha == acess.senha){
                    cout<<"o senha esta : "<<it->senha<<endl;
                    cout<<"por favor informe a funcao: ";
                    cin>>acess.funcao;
                    for(it = contas.begin(); it!= contas.end(); ++it){
                        cout<<"o funcao esta : "<<it->funcao<<endl;
                        if(it->funcao == acess.funcao && it->funcao == "secretario")return 2;
                        else if(it->funcao == acess.funcao && it->funcao == "operador")return 3;
                    }
                        cout<<"funcao incorreta"<<endl;
                        break;
                }
            }
            cout<<"senha incorreta,insira os dados novamente"<<endl;
            break;
        }

    }
    cout<<"Nome de usuario incorreto,tente novamente"<<endl;
    login();

}

bool criar_usuario(){
    usuario b;
    int deci;
    cout<<"Digite um nome de usuario: ";
    cin>>b.nome;
    cout<<"Digite uma senha: ";
    cin>>b.senha;
    cout<<"Digite sua funcao: ";
    cin>>b.funcao;

    cout<<"digite 1 para cadastrar e fazer login ou 2 para cancelar e voltar a tela de login"<<endl;
    cin>>deci;
    if(deci== 1 ){
        contas.push_back(b);
        return true;
    }if(deci == 2)
        return false;
}

void alterar_usuario(){
    usuario b;
    int m;
cout<<"se deseja alterar o nome digite 1"<<endl;
cout<<"se deseja alterar a senha digite 2"<<endl;
cout<<"se deseja alterar a funcao digite 3"<<endl;
cout<<"se deseja salvar digite 4"<<endl;
cout<<"se deseja cancelar e voltar ao login digite 5"<<endl;

    cin>>m;
    switch(m){

        case 1:
            cout<<"por favor digite o nome atual: ";
            cin>>b.nome;
            for(it = contas.begin(); it!= contas.end(); ++it){
                if(it->nome == b.nome){
                    cout<<"digite o novo nome: ";
                    cin>>b.nome;
                    it->nome = b.nome;
                    cout<<"nome alterado com sucesso para: "<<it->nome<<endl;
                    login();
                }
            }
            cout<<"nome nao encontrado";
            alterar_usuario();
        case 2:
            cout<<"por favor digite a senha atual: ";
            cin>>b.senha;
            for(it = contas.begin(); it!= contas.end(); ++it){
                if(it->senha == b.senha){
                    cout<<"digite a nova senha: ";
                    cin>>b.senha;
                    it->senha = b.senha;
                    break;
                }
            }
            cout<<"senha nao esta correta"<<endl;
            break;
        case 3:
            cout<<"por favor digite a funcao atual: ";
            cin>>b.funcao;
            for(it = contas.begin(); it!= contas.end(); ++it){
                if(it->funcao == b.funcao){
                    cout<<"digite a nova funcao: ";
                    cin>>b.funcao;
                    it->funcao = b.funcao;
                    break;
                }
            }
            cout<<"funcao nao esta correta"<<endl;
            break;
        case 4:
            login();
            break;
        case 5:
            login();
            break;
    }

}

void excluir_usuario(){
    usuario a;
    cout<<"digite o nome de usuario que deseja excluir ou digite 2 para cancelar: ";
    cin>>a.nome;
    if(a.nome=="2")login();
       for(it = contas.begin(); it!= contas.end(); ++it){
                if(it->nome == a.nome){
                        contas.pop_back();
                        cout<<"conta apagada"<<endl;
                        login();
                }
       }
       cout<<"usuario nao encontrado"<<endl;
       excluir_usuario();

}



int main(){

int menu;
int retorno = 5;

    if(login()== 3 && retorno == 5){
        cout<<"_________MENU_________"<<endl;
        cout<<"Digite 1 para criar usuario"<<endl;
        cout<<"Digite 2 para alterar usuario"<<endl;
        cout<<"Digite 3 para excluir usuario"<<endl;
        cin>>menu;
        switch(menu){

            case 1:
                if(criar_usuario()==true){
                    cout<<"usuario criado com sucesso."<<endl;
                    retorno == 2;
                    return main();

                }else
                    return main();

            case 2:
                alterar_usuario();
                retorno == 2;
                return main();


            case 3:
                excluir_usuario();
                retorno == 2;
                return main();

        }
        return main();
    }
    else if(login()==2){
        cout<<"bug";
    }
return 0;

}
