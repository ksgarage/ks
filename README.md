# MODELOS
from datetime import datetime, timedelta

class Livro:
def __init__(self, titulo, autor, isbn, quantidade):
self.titulo = titulo
self.autor = autor
self.isbn = isbn
self.quantidade_total = quantidade
self.quantidade_disponivel = quantidade

def emprestar(self):
if self.quantidade_disponivel > 0:
self.quantidade_disponivel -= 1
return True
return False

def devolver(self):
if self.quantidade_disponivel < self.quantidade_total:
self.quantidade_disponivel += 1

class Usuario:
def __init__(self, nome, user_id):
self.nome = nome
self.user_id = user_id
self.emprestimos = []

class Emprestimo:
def __init__(self, livro, usuario):
self.livro = livro
self.usuario = usuario
self.data_emprestimo = datetime.now()
self.data_prevista_devolucao = self.data_emprestimo + timedelta(days=7)
self.data_devolucao = None

def devolver(self):
self.data_devolucao = datetime.now()
self.livro.devolver()

class RepositorioLivros:
def __init__(self):
self.livros = {}

def adicionar_livro(self, livro):
self.livros[livro.isbn] = livro

def buscar_por_isbn(self, isbn):
return self.livros.get(isbn, None)

def listar_livros(self):
return list(self.livros.values())

class RepositorioUsuarios:
def __init__(self):
self.usuarios = {}

def adicionar_usuario(self, usuario):
self.usuarios[usuario.user_id] = usuario

def buscar_por_id(self, user_id):
return self.usuarios.get(user_id, None)

class SistemaBiblioteca:
def __init__(self):
self.repo_livros = RepositorioLivros()
self.repo_usuarios = RepositorioUsuarios()

def cadastrar_livro(self, titulo, autor, isbn, quantidade):
livro = Livro(titulo, autor, isbn, quantidade)
self.repo_livros.adicionar_livro(livro)

def cadastrar_usuario(self, nome, user_id):
usuario = Usuario(nome, user_id)
self.repo_usuarios.adicionar_usuario(usuario)

def emprestar_livro(self, user_id, isbn):
usuario = self.repo_usuarios.buscar_por_id(user_id)
livro = self.repo_livros.buscar_por_isbn(isbn)
if usuario and livro and livro.emprestar():
emprestimo = Emprestimo(livro, usuario)
usuario.emprestimos.append(emprestimo)
print("✅ Empréstimo realizado com sucesso!")
else:
print("⚠️ Não foi possível realizar o empréstimo.")

def devolver_livro(self, user_id, isbn):
usuario = self.repo_usuarios.buscar_por_id(user_id)
if usuario:
for emp in usuario.emprestimos:
if emp.livro.isbn == isbn and emp.data_devolucao is None:
emp.devolver()
print("✅ Livro devolvido com sucesso!")
return
print("⚠️ Empréstimo não encontrado.")

# Criando o sistema
sistema = SistemaBiblioteca()

# Cadastrando dados iniciais
sistema.cadastrar_livro("Python na Prática", "Ana Silva", "1234", 3)
sistema.cadastrar_usuario("Carlos Mendes", "u001")

# Realizando empréstimo
sistema.emprestar_livro("u001", "1234")

# Listando livros
for livro in sistema.repo_livros.listar_livros():
print(f"{livro.titulo} ({livro.isbn}) - Disponíveis: {livro.quantidade_disponivel}")

# Devolvendo livro
sistema.devolver_livro("u001", "1234")

class SistemaBiblioteca:
def __init__(self):
self.repo_livros = RepositorioLivros()
self.repo_usuarios = RepositorioUsuarios()

def obter_dados_livro(self):
titulo = input("Digite o título do livro: ")
autor = input("Digite o autor do livro: ")
isbn = input("Digite o ISBN do livro: ")
quantidade = int(input("Digite a quantidade de exemplares: "))
return titulo, autor, isbn, quantidade

def obter_dados_usuario(self):
nome = input("Digite o nome do usuário: ")
user_id = input("Digite o ID do usuário: ")
return nome, user_id

def cadastrar_livro_interativo(self):
titulo, autor, isbn, quantidade = self.obter_dados_livro()
self.cadastrar_livro(titulo, autor, isbn, quantidade)
print("✅ Livro cadastrado com sucesso!")

def cadastrar_usuario_interativo(self):
nome, user_id = self.obter_dados_usuario()
self.cadastrar_usuario(nome, user_id)
print("✅ Usuário cadastrado com sucesso!")

def gerar_relatorio_emprestimos(self):
print("Relatório de Empréstimos:")
for usuario in self.repo_usuarios.usuarios.values():
for emprestimo in usuario.emprestimos:
if emprestimo.data_devolucao is None:
print(f"- {emprestimo.livro.titulo} emprestado para {emprestimo.usuario.nome} (Devolução prevista: {emprestimo.data_prevista_devolucao.strftime('%d/%m/%Y')})")

def exibir_menu(self):
print("\n--- Sistema da Biblioteca ---")
print("1. Cadastrar Livro")
print("2. Cadastrar Usuário")
print("3. Emprestar Livro")
print("4. Devolver Livro")
print("5. Listar Livros")
print("6. Gerar Relatório de Empréstimos")
print("7. Sair")
opcao = input("Escolha uma opção: ")
return opcao

def executar_opcao(self, opcao):
if opcao == "1":
self.cadastrar_livro_interativo()
elif opcao == "2":
self.cadastrar_usuario_interativo()
elif opcao == "3":
user_id = input("Digite o ID do usuário: ")
isbn = input("Digite o ISBN do livro: ")
self.emprestar_livro(user_id, isbn)
elif opcao == "4":
user_id = input("Digite o ID do usuário: ")
isbn = input("Digite o ISBN do livro: ")
self.devolver_livro(user_id, isbn)
elif opcao == "5":
for livro in self.repo_livros.listar_livros():
print(f"{livro.titulo} ({livro.isbn}) - Disponíveis: {livro.quantidade_disponivel}")
elif opcao == "6":
self.gerar_relatorio_emprestimos()
elif opcao == "7":
print("Saindo do sistema...")
else:
print("Opção inválida!")

def iniciar(self):
while True:
opcao = self.exibir_menu()
if opcao == "7":
break
self.executar_opcao(opcao)

# Criando o sistema
sistema = SistemaBiblioteca()

# Iniciando o sistema
sistema.iniciar()
