# 🌆 Sentinela Urbana

![Status do Projeto: Em Desenvolvimento](https://img.shields.io/badge/status-em_desenvolvimento-yellow)
![Flutter: v3.x](https://img.shields.io/badge/Frontend-Flutter-blue?logo=flutter)
![FastAPI: Python](https://img.shields.io/badge/Backend-FastAPI-green?logo=fastapi)
![Database: PostGIS](https://img.shields.io/badge/Database-PostGIS-blue?logo=postgresql)

Projeto de **Atividade Prática Supervisionada (APS)** para um sistema distribuído de gerenciamento de informações ambientais urbanas, utilizando *crowdsourcing* através de um aplicativo móvel.

---

## ✨ Funcionalidades (Fases 1 e 2)

* **Autenticação de Usuário:** Registro (`/auth/register`) e Login (`/auth/login`) com senhas criptografadas (`bcrypt`) e autenticação via tokens JWT.
* **Mapa Interativo:** Visualização de relatos em tempo real com **OpenStreetMap** via `flutter_map`.
* **Geolocalização (GPS):** Centralização automática no ponto atual do usuário (`geolocator`).
* **Criação de Relatos (POST):** Envio de novos relatos (alagamento, trânsito, etc.) com marcação no mapa.
* **Visualização de Relatos (GET):** Ícones personalizados por categoria exibidos no mapa.
* **Arquitetura Limpa:** Uso de *Clean Architecture*, gerenciamento de estado com **BLoC** e repositórios para acesso a dados.

---

## 🛠️ Tecnologias Utilizadas

### Frontend (Mobile)

* **[Flutter](https://flutter.dev/)**
* **[flutter_bloc](https://bloclibrary.dev/)**
* **[flutter_map](https://docs.fleaflet.dev/)**
* **[geolocator](https://pub.dev/packages/geolocator)**
* **[flutter_secure_storage](https://pub.dev/packages/flutter_secure_storage)**
* **[http](https://pub.dev/packages/http)**

### Backend (API)

* **[FastAPI](https://fastapi.tiangolo.com/)**
* **[SQLAlchemy](https://www.sqlalchemy.org/)**
* **[Pydantic V2](https://docs.pydantic.dev/latest/)**
* **[Passlib (bcrypt)](https://passlib.readthedocs.io/en/stable/)**
* **[python-jose](https://github.com/mpdavis/python-jose)**

### Banco de Dados

* **[PostgreSQL](https://www.postgresql.org/)** com **[PostGIS](https://postgis.net/)**
* **[Docker](https://www.docker.com/)** (para rodar o contêiner PostGIS)

---

## 🚀 Como Executar o Projeto

### Pré-requisitos

* Flutter SDK (v3.x)
* Python (v3.10+)
* Docker Desktop (rodando)

---

## 1. Configuração do Backend (Servidor)

```bash
# 1. Navegue até a pasta raiz do projeto
cd /caminho/para/SentinelaUrbana

# 2. Crie e ative o ambiente virtual
python -m venv venv
# Windows
.\venv\Scripts\activate
# Mac/Linux
source venv/bin/activate

# 3. Instale as dependências
pip install -r requirements.txt

# 4. Navegue até a pasta do backend
cd backend

# 5. Inicie o contêiner do banco (PostGIS)
docker compose up -d

# 6. Volte para a raiz e inicie o servidor FastAPI
cd ..
python -m uvicorn backend.main:app --reload
```

O backend estará disponível em: **[http://127.0.0.1:8000](http://127.0.0.1:8000)**

---

## 2. Configuração do Frontend (App)

```bash
# 1. Em um NOVO terminal, navegue até a pasta do app
cd /caminho/para/SentinelaUrbana/frontend/sentinela_urbana

# 2. Instale os pacotes do Flutter
flutter pub get
```

### Configuração da URL da API

Abra os arquivos:

* `lib/data/repositories/report_repository_impl.dart`
* `lib/data/repositories/auth_repository_impl.dart`

E garanta que `_baseUrl` está correta para o ambiente:

```dart
// Para rodar no navegador (Web)
static const String _baseUrl = 'http://127.0.0.1:8000';

// Para rodar no Emulador Android
static const String _baseUrl = 'http://10.0.2.2:8000';
```

### Permissões de GPS (Android)

Verifique o arquivo `android/app/src/main/AndroidManifest.xml` para as permissões de localização necessárias.

### Executar o app

```bash
flutter run
```

---

## 📋 Endpoints da API

| Método |     Endpoint     | Descrição                            |
| :----: | :--------------: | :----------------------------------- |
| `POST` | `/auth/register` | Registra um novo usuário             |
| `POST` |   `/auth/login`  | Autentica e retorna um token JWT     |
|  `GET` |   `/v1/reports`  | Retorna todos os relatos (protegido) |
| `POST` |   `/v1/reports`  | Cria um novo relato (protegido)      |

---

## 📌 Estrutura do Projeto

```
SentinelaUrbana/
├── backend/
│   ├── main.py
│   ├── routers/
│   ├── models/
│   ├── schemas/
│   └── docker-compose.yml
├── frontend/
│   └── sentinela_urbana/
│       ├── lib/
│       ├── assets/
│       └── pubspec.yaml
└── README.md
```

---

## 🔮 Futuras Implementações (ideias)

* Upload de fotos e anexos nos relatos.
* Notificações push para atualizações/alertas na região.
* Filtragem e pesquisa avançada por categoria, data e distância.
* Sistema de moderação / verificação de relatos.
* Dashboard web com estatísticas e heatmaps.

---

## 🤝 Contribuição

Contribuições são bem-vindas!

1. Faça um fork deste repositório.
2. Crie uma branch com sua feature: `git checkout -b feature/nome-da-sua-feature`
3. Commit suas mudanças: `git commit -m "Descrição curta"`
4. Envie para o repositório remoto: `git push origin feature/nome-da-sua-feature`
5. Abra um Pull Request.

Por favor, descreva claramente o propósito da contribuição e inclua instruções para testar localmente.
