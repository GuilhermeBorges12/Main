# NEXUSCART — MEU TRABALHO (INTEGRANTE 1 • BACK-END: CORE & PRODUTOS) Guilherme Borges Rocha

Aplicação e-commerce Full-Stack (MERN) com cadastro/login, vitrine, carrinho e pedidos.  
**Stack:** Node.js/Express 5, MongoDB/Mongoose, JWT/Bcrypt, React + Vite, Axios.

---

## 👤 MINHA CONTRIBUIÇÃO (EXCLUSIVA — INTEGRANTE 1)

**Escopo:** infraestrutura do back-end e domínio **Produtos**.

### O que eu fiz
- **Boot do servidor:** configuração do **Express 5**, **CORS**, `express.json()` e rotas base / healthcheck.
- **Conexão MongoDB Atlas:** módulo `config/db.js` com `mongoose.connect`.
- **Modelo de Produto (`models/Product.js`):**  
  `name`, `description`, `price`, `stock`, `categories[]`, `images[]`, `isActive`, timestamps.
- **API de Produtos (`routes/productRoutes.js`):**
  - `POST /api/products` — criar produto  
  - `GET /api/products` — paginação, busca (`?q=`), **categoria**, **faixa de preço** e **ordenação** (`?sort=price|-price|createdAt|-createdAt`)  
  - `GET /api/products/:id` — detalhe  
  - `PUT /api/products/:id` — atualização com validações  
  - `PATCH /api/products/:id/stock` — ajuste de estoque (delta)  
  - `DELETE /api/products/:id` — **soft delete** (`isActive=false`)  
  - `PATCH /api/products/:id/restore` — restaura  
  - `GET /api/products/categories/all` — categorias únicas (para filtros no front)
- **Integração no `server.js`:** `app.use('/api/products', productRoutes)`.
- **Upload de imagens (opcional):** `uploadRoutes.js` + `app.use('/uploads', express.static(...))`.
- **Seed de dados:** `src/seeds/seed.js` (cria admin, usuário e produtos exemplo; não duplica).
- **Boas práticas:** `.env` não versionado + `.env.example`, `JWT_SECRET`, `CORS_ORIGIN`, `UPLOAD_DIR`.

### Como minha parte se integra
- O **Front** usa a listagem/detalhe de produtos, filtros por **categorias** e **ordenação**, e o `_id` para “Adicionar ao carrinho”.
- O módulo de **Pedidos** consome **preço/estoque** dos produtos e abate/devolve estoque em pagamento/cancelamento.

---

## 🔌 ROTAS PRINCIPAIS PARA TESTE

GET /api/products?page=1&limit=12&q=camiseta&category=roupas&sort=-createdAt
GET /api/products/:id
POST /api/products
PUT /api/products/:id
PATCH /api/products/:id/stock body: { "delta": 2 }
DELETE /api/products/:id (soft delete)
PATCH /api/products/:id/restore
GET /api/products/categories/all


---

## 📌 COMMITS RELEVANTES (EXEMPLOS)

- `feat(products): CRUD, paginação, busca, filtros e ordenação`
- `feat(server): boot do express, CORS e wiring das rotas`
- `feat(upload): servir /uploads e criar uploadRoutes`
- `chore(seed): admin/cliente e produtos de exemplo`


## 🛠️ COMO RODAR LOCALMENTE

> Requisitos: **Node 20.19+** (ou 22.12+) e **MongoDB Atlas**.

```bash
# Backend
cd backend
cp .env.example .env    # ajuste MONGO_URI, JWT_SECRET etc.
npm i
npm run dev             # ou: node src/server.js

# (opcional) popular dados
npm run seed

# Frontend (outro terminal)
cd ../frontend
echo VITE_API_URL=http://localhost:4000 > .env
npm i
npm run dev

---
