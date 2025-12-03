# Contexto do Projeto: FRP

Este arquivo contém o contexto técnico e regras de negócio para auxiliar o Gemini na geração de código e sugestões.

## 🛠 Tech Stack & Versões Principais
O projeto é um backend API RESTful.
- **Linguagem:** Python (Tipagem estática encorajada devido ao `mypy`).
- **Framework:** Django 4.2.4.
- **API Toolkit:** Django REST Framework (DRF) 3.14.0.
- **Banco de Dados:** MySQL (`mysqlclient`).
- **Autenticação:** JWT (`djangorestframework-simplejwt`).
- **Filtros:** `django-filter`.
- **Qualidade de Código:** `mypy` (type checking), `pycodestyle`, `pyflakes`.

## 📏 Regras de Codificação (Style Guide)

### 1. Tipagem e Qualidade (Crucial)
Como o projeto utiliza **mypy**, todo código novo deve conter *type hints*.
- **Correto:** `def calcular_total(preco: float, qtd: int) -> float:`
- **Incorreto:** `def calcular_total(preco, qtd):`

### 2. Estrutura do Django REST Framework (DRF)
- **Views:** Priorize `ModelViewSet` para CRUDs padrão. Use `APIView` apenas para endpoints que fogem muito do padrão REST.
- **Serializers:** Use `ModelSerializer` sempre que possível.
- **Filtros:** Utilize `DjangoFilterBackend` para filtragem em listagens, em vez de filtrar manualmente na queryset.

### 3. Autenticação & Segurança
- O sistema usa **SimpleJWT**.
- Endpoints protegidos devem ter `permission_classes = [IsAuthenticated]`.
- Lembre-se das configurações de CORS (`django-cors-headers`) ao sugerir conexões com o Frontend.

### 4. Modelagem de Dados (MySQL)
- Evite campos `JSONField` se possível (para manter compatibilidade estrita e performance no MySQL, a menos que estritamente necessário).
- Use `snake_case` para nomes de campos e `CamelCase` para nomes de Models.

## 🤖 Instruções para o Gemini
1. **Geração de Código:** Ao fornecer snippets, inclua os imports necessários do `rest_framework`, `typing`, etc.
2. **Settings:** Se sugerir alterações no `settings.py`, verifique se não conflita com `django-cors-headers` ou `simplejwt`.
3. **Testes:** Se solicitado testes, use `APITestCase` do DRF.