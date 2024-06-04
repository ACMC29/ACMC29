
import json

# Função para carregar contatos de um arquivo JSON
def carregar_contatos(arquivo):
    try:
        with open(arquivo, 'r') as f:
            return json.load(f)
    except FileNotFoundError:
        return []
    except json.JSONDecodeError:
        return []

# Função para salvar contatos em um arquivo JSON
def salvar_contatos(arquivo, contatos):
    with open(arquivo, 'w') as f:
        json.dump(contatos, f, indent=4)

# Função para cadastrar um novo contato
def cadastrar_contato(contatos):
    nome = input("Nome: ")
    telefone = input("Telefone: ")
    email = input("Email: ")
    contatos.append({'nome': nome, 'telefone': telefone, 'email': email})
    print("Contato cadastrado com sucesso!")

# Função para pesquisar um contato por nome ou telefone
def pesquisar_contato(contatos):
    termo = input("Digite o nome ou telefone para pesquisar: ")
    resultados = [contato for contato in contatos if termo in contato['nome'] or termo in contato['telefone']]
    if resultados:
        for contato in resultados:
            print(f"Nome: {contato['nome']}, Telefone: {contato['telefone']}, Email: {contato['email']}")
    else:
        print("Nenhum contato encontrado.")

# Função para listar todos os contatos
def listar_contatos(contatos):
    if contatos:
        for contato in contatos:
            print(f"Nome: {contato['nome']}, Telefone: {contato['telefone']}, Email: {contato['email']}")
    else:
        print("Nenhum contato para listar.")

# Função para editar um contato
def editar_contato(contatos):
    nome = input("Digite o nome do contato a ser editado: ")
    for contato in contatos:
        if contato['nome'] == nome:
            contato['telefone'] = input(f"Novo telefone para {contato['nome']}: ")
            contato['email'] = input(f"Novo email para {contato['nome']}: ")
            print("Contato atualizado com sucesso!")
            return
    print("Contato não encontrado!")

# Função para excluir um contato
def excluir_contato(contatos):
    nome = input("Digite o nome do contato a ser excluído: ")
    for contato in contatos:
        if contato['nome'] == nome:
            contatos.remove(contato)
            print("Contato excluído com sucesso!")
            return
    print("Contato não encontrado!")

# Função principal para o menu
def menu():
    arquivo = 'contatos.json'
    contatos = carregar_contatos(arquivo)

    while True:
        print("\n--- Lista Telefônica ---")
        print("1. Cadastrar um contato")
        print("2. Pesquisar um contato (nome ou telefone)")
        print("3. Listar todos os contatos")
        print("4. Editar um contato")
        print("5. Excluir um contato")
        print("6. Sair")

        opcao = input("Escolha uma opção: ")

        if opcao == '1':
            cadastrar_contato(contatos)
        elif opcao == '2':
            pesquisar_contato(contatos)
        elif opcao == '3':
            listar_contatos(contatos)
        elif opcao == '4':
            editar_contato(contatos)
        elif opcao == '5':
            excluir_contato(contatos)
        elif opcao == '6':
            salvar_contatos(arquivo, contatos)
            print("Lista salva. Saindo...")
            break
        else:
            print("Opção inválida! Tente novamente.")

if __name__ == "__main__":
    menu()
