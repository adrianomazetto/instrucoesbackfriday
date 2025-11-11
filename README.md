Vamos criar o BACKEND do site BACK FRIDAY

![image.png](attachment:51925851-990d-44e1-b021-778a8b3a4b81:image.png)

1º abra o vscode

# **crie o arquivo index.html**

```html
<!doctype html>
<html lang="pt-BR">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Back Friday</title>
    <link rel="stylesheet" href="styles.css">
  </head>
  <body>
  <canvas id="particles-canvas"></canvas>
    <main>
      <section class="hero-section">
        <div class="hero-content">
          <h1 class="main-title" id="main-title">BACK FRIDAY</h1>
          <p class="subtitle" id="subtitle">Descontos de até 70%</p>
          <div class="countdown-container">
            <div class="countdown-item">
              <span class="countdown-number" id="days">00</span>
              <span class="countdown-label">Dias</span>
            </div>
            <div class="countdown-item">
              <span class="countdown-number" id="hours">00</span>
              <span class="countdown-label">Horas</span>
            </div>
            <div class="countdown-item">
              <span class="countdown-number" id="minutes">00</span>
              <span class="countdown-label">Minutos</span>
            </div>
            <div class="countdown-item">
              <span class="countdown-number" id="seconds">00</span>
              <span class="countdown-label">Segundos</span>
            </div>
          </div>
        </div>
      </section>
      <section class="products-section">
        <!-- Título e grade de produtos. O JS insere cartões de produto aqui. -->
        <h2 class="products-title">Ofertas Imperdíveis</h2>
        <div class="products-grid"></div>
      </section>
    </main>
    <script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>
    <script>
    window.__SUPABASE = window.__SUPABASE || {
        url: window.SUPABASE_URL || 'https://seuenderecourlaqui.supabase.co',
        anonKey: window.SUPABASE_ANON_KEY || 'abcdefg1234...'
      };
    </script>
    <script src="script.js"></script>
  </body>
</html>
```

# **crie o arquivo styles.css**

```css
/*
  Folha de estilos principal do projeto.
  Objetivo: aparência clara e moderna, com destaque para o tema verde.
  Comentários didáticos explicam o papel de cada bloco.
*/

body {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-family: 'Arial', sans-serif;
  background: #000000;
  color: #ffffff;
  overflow-x: hidden;
  height: 100%;
}

html {
  height: 100%;
}

* {
  box-sizing: border-box;
}

#particles-canvas {
  /* Canvas fixo no fundo para animação de partículas */
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 0;
  pointer-events: none;
}

.hero-section {
  /* Seção hero: título grande, subtítulo e contador */
  position: relative;
  min-height: 60%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 60px 20px;
  overflow: hidden;
}

.hero-content {
  /* Conteúdo central, acima do canvas (z-index) */
  position: relative;
  z-index: 2;
  text-align: center;
  max-width: 900px;
}

.main-title {
  /* Título principal com efeito de brilho e pulsação */
  font-size: 72px;
  font-weight: bold;
  margin: 0 0 20px 0;
  letter-spacing: 8px;
  text-shadow: 0 0 20px rgba(49, 234, 137, 0.8);
  animation: pulse 2s ease-in-out infinite;
}

@keyframes pulse {
  0%, 100% { transform: scale(1); }
  50% { transform: scale(1.05); }
}

.subtitle {
  /* Subtítulo abaixo do H1 */
  font-size: 28px;
  margin: 0 0 40px 0;
  opacity: 0.9;
}

.countdown-container {
  /* Contêiner dos números do contador */
  display: flex;
  gap: 20px;
  justify-content: center;
  flex-wrap: wrap;
  margin-top: 30px;
}

.countdown-item {
  /* Cartões do contador, com fundo translúcido e borda verde */
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  border: 2px solid #31EA89;
  border-radius: 12px;
  padding: 20px 30px;
  min-width: 120px;
  box-shadow: 0 8px 32px rgba(49, 234, 137, 0.3);
}

.countdown-number {
  /* Número grande do contador */
  font-size: 48px;
  font-weight: bold;
  color: #31EA89;
  display: block;
  line-height: 1;
}

.countdown-label {
  /* Rótulo abaixo do número (Dias, Horas...) */
  font-size: 14px;
  text-transform: uppercase;
  margin-top: 8px;
  opacity: 0.8;
  letter-spacing: 2px;
}

.products-section {
  /* Seção dos produtos; z-index 2 para ficar acima do canvas */
  position: relative;
  z-index: 2;
  padding: 60px 20px;
  background: transparent;
}

.products-title {
  /* Título da seção de produtos */
  text-align: center;
  font-size: 42px;
  font-weight: bold;
  margin: 0 0 50px 0;
  color: #31EA89;
}

.products-grid {
  /* Grade responsiva que se adapta ao tamanho da tela */
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 30px;
  max-width: 1200px;
  margin: 0 auto;
}

.product-card {
  /* Cartão de produto com hover animado */
  background: #1a1a1a;
  border-radius: 16px;
  overflow: hidden;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  border: 2px solid transparent;
}

.product-card:hover {
  transform: translateY(-10px);
  box-shadow: 0 20px 40px rgba(49, 234, 137, 0.4);
  border-color: #31EA89;
}

.product-image {
  /* Área da imagem do produto: usamos emoji centralizado */
  width: 100%;
  height: 250px;
  background: linear-gradient(135deg, #2a2a2a 0%, #1a1a1a 100%);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 80px;
  position: relative;
}

.discount-badge {
  /* Selo de desconto no canto superior direito */
  position: absolute;
  top: 15px;
  right: 15px;
  background: #31EA89;
  color: #ffffff;
  padding: 8px 16px;
  border-radius: 25px;
  font-weight: bold;
  font-size: 16px;
  box-shadow: 0 4px 12px rgba(49, 234, 137, 0.5);
}

.product-info {
  /* Conteúdo textual do produto */
  padding: 25px;
}

.product-name {
  /* Nome do produto */
  font-size: 24px;
  font-weight: bold;
  margin: 0 0 15px 0;
  color: #ffffff;
}

.price-container {
  /* Linha com preço antigo e novo */
  display: flex;
  align-items: center;
  gap: 15px;
  margin-bottom: 20px;
}

.old-price {
  /* Preço antigo riscado, com menos destaque */
  font-size: 18px;
  text-decoration: line-through;
  opacity: 0.5;
}

.new-price {
  /* Preço novo em destaque (verde) */
  font-size: 32px;
  font-weight: bold;
  color: #31EA89;
}

.buy-button {
  /* Botão de compra ocupando toda a largura */
  width: 100%;
  padding: 15px;
  background: #31EA89;
  color: #ffffff;
  border: none;
  border-radius: 8px;
  font-size: 18px;
  font-weight: bold;
  cursor: pointer;
  transition: background 0.3s ease, transform 0.2s ease;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.buy-button:hover {
  /* Efeito visual ao passar o mouse no botão */
  background: #28d878;
  transform: translateY(-2px);
}

/* Responsividade simples: ajusta espaçamentos em telas menores */
  /* Responsividade simples: ajusta espaçamentos em telas menores */
@media (max-width: 768px) {
  .main-title { font-size: 48px; letter-spacing: 4px; }
  .subtitle { font-size: 22px; }
  .product-image { height: 200px; font-size: 64px; }
}

@media (max-width: 480px) {
  .main-title { font-size: 38px; letter-spacing: 2px; }
  .subtitle { font-size: 18px; }
  .products-grid { gap: 20px; }
}

.buy-button:hover {
  background: #28c970;
  transform: scale(1.05);
}

.buy-button:active {
  transform: scale(0.98);
}

@media (max-width: 768px) {
  .main-title {
    font-size: 48px;
    letter-spacing: 4px;
  }

  .subtitle {
    font-size: 20px;
  }

  .countdown-item {
    min-width: 90px;
    padding: 15px 20px;
  }

  .countdown-number {
    font-size: 36px;
  }
  .countdown-label {
    font-size: 12px;
  }
}

@media (max-width: 768px) {
  .main-title { font-size: 48px; letter-spacing: 4px; }
  .subtitle { font-size: 22px; }
  .product-image { height: 200px; font-size: 64px; }
}

@media (max-width: 480px) {
  .main-title { font-size: 38px; letter-spacing: 2px; }
  .subtitle { font-size: 18px; }
  .products-grid { gap: 20px; }
}

.buy-button:hover {
  background: #28c970;
  transform: scale(1.05);
}

.buy-button:active {
  transform: scale(0.98);
}

@media (max-width: 768px) {
  .main-title {
    font-size: 48px;
    letter-spacing: 4px;
  }

  .subtitle {
    font-size: 20px;
  }

  .countdown-item {
    min-width: 90px;
    padding: 15px 20px;
  }

  .countdown-number {
    font-size: 36px;
  }
  .countdown-label {
    font-size: 12px;
  }
}

```

# **crie o arquivo script.js**

```jsx
// ================================================
// Arquivo: script.js
// Objetivo: controlar animações, contador e carregamento de produtos.
// Fluxo principal de dados: Supabase -> Fallback para mock.
// Linguagem simples e didática para alunos.
// ================================================

// ------------------------------
// Contador regressivo (Countdown)
// Define uma data futura (3 dias a partir de agora) e
// atualiza os números na tela a cada segundo.
const countdownDate = new Date();
countdownDate.setDate(countdownDate.getDate() + 3);
countdownDate.setHours(23, 59, 59, 999);

function updateCountdown() {
  const now = new Date().getTime();
  const distance = countdownDate - now;

  const days = Math.floor(distance / (1000 * 60 * 60 * 24));
  const hours = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
  const minutes = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60));
  const seconds = Math.floor((distance % (1000 * 60)) / 1000);

  document.getElementById('days').textContent = String(days).padStart(2, '0');
  document.getElementById('hours').textContent = String(hours).padStart(2, '0');
  document.getElementById('minutes').textContent = String(minutes).padStart(2, '0');
  document.getElementById('seconds').textContent = String(seconds).padStart(2, '0');

  if (distance < 0) {
    document.getElementById('days').textContent = '00';
    document.getElementById('hours').textContent = '00';
    document.getElementById('minutes').textContent = '00';
    document.getElementById('seconds').textContent = '00';
  }
}

updateCountdown();
setInterval(updateCountdown, 1000);

// ------------------------------
// Animação de partículas (visual de fundo)
// Usamos um <canvas> para desenhar pontos e linhas que se movimentam.
// Isso é puramente estético para deixar a página mais atrativa.
const canvas = document.getElementById('particles-canvas');
const ctx = canvas.getContext('2d');

function resizeCanvas() {
  canvas.width = window.innerWidth;
  canvas.height = Math.max(document.body.scrollHeight, window.innerHeight);
}

resizeCanvas();

const particles = [];
const particleCount = 150;

class Particle {
  constructor() {
    this.x = Math.random() * canvas.width;
    this.y = Math.random() * canvas.height;
    this.vx = (Math.random() - 0.5) * 2;
    this.vy = (Math.random() - 0.5) * 2;
    this.radius = Math.random() * 3 + 2;
  }

  update() {
    this.x += this.vx;
    this.y += this.vy;

    if (this.x < 0 || this.x > canvas.width) this.vx *= -1;
    if (this.y < 0 || this.y > canvas.height) this.vy *= -1;
  }

  draw() {
    ctx.beginPath();
    ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2);
    ctx.fillStyle = 'rgba(49, 234, 137, 0.5)';
    ctx.fill();
  }
}

for (let i = 0; i < particleCount; i++) {
  particles.push(new Particle());
}

function connectParticles() {
  for (let i = 0; i < particles.length; i++) {
    for (let j = i + 1; j < particles.length; j++) {
      const dx = particles[i].x - particles[j].x;
      const dy = particles[i].y - particles[j].y;
      const distance = Math.sqrt(dx * dx + dy * dy);

      if (distance < 120) {
        ctx.beginPath();
        ctx.strokeStyle = `rgba(49, 234, 137, ${0.4 * (1 - distance / 120)})`;
        ctx.lineWidth = 1;
        ctx.moveTo(particles[i].x, particles[i].y);
        ctx.lineTo(particles[j].x, particles[j].y);
        ctx.stroke();
      }
    }
  }
}

function animate() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);

  particles.forEach(particle => {
    particle.update();
    particle.draw();
  });

  connectParticles();

  requestAnimationFrame(animate);
}

animate();

window.addEventListener('resize', resizeCanvas);

// Update canvas height when content changes
const resizeObserver = new ResizeObserver(resizeCanvas);
resizeObserver.observe(document.body);

// Also update on scroll to ensure full coverage
let scrollTimeout;
window.addEventListener('scroll', () => {
  clearTimeout(scrollTimeout);
  scrollTimeout = setTimeout(resizeCanvas, 100);
});

function formatBRL(value) {
  // Formata um número para moeda brasileira (R$)
  const num = Number(value);
  if (Number.isNaN(num)) return 'R$ 0,00';
  return num.toLocaleString('pt-BR', { style: 'currency', currency: 'BRL' });
}

function escapeHtml(str) {
  // Evita problemas de segurança ao inserir texto no HTML,
  // convertendo caracteres especiais em entidades.
  return String(str)
    .replace(/&/g, '&amp;')
    .replace(/</g, '&lt;')
    .replace(/>/g, '&gt;')
    .replace(/"/g, '&quot;')
    .replace(/'/g, '&#39;');
}

function showToast(message) {
  // Exibe uma mensagem de feedback temporária no canto da tela.
  const messageDiv = document.createElement('div');
  messageDiv.textContent = message;
  messageDiv.style.cssText = `
    position: fixed;
    top: 20px;
    right: 20px;
    background: #31EA89;
    color: white;
    padding: 15px 25px;
    border-radius: 8px;
    font-weight: bold;
    z-index: 1000;
    box-shadow: 0 4px 12px rgba(0,0,0,0.3);
    animation: slideIn 0.3s ease;
  `;
  document.body.appendChild(messageDiv);
  setTimeout(() => {
    messageDiv.style.animation = 'slideOut 0.3s ease';
    setTimeout(() => messageDiv.remove(), 300);
  }, 2000);
}

function attachBuyButtonHandlers() {
  // Adiciona comportamento ao botão "Comprar Agora" de cada produto.
  // Aqui apenas mostramos um toast simulando a adição ao carrinho.
  document.querySelectorAll('.buy-button').forEach(button => {
    button.addEventListener('click', function() {
      const productName = this.closest('.product-card').querySelector('.product-name').textContent;
      showToast(`${productName} adicionado ao carrinho!`);
    });
  });
}

function renderProducts(products) {
  // Recebe uma lista de produtos e cria os cartões na grade.
  // Cada cartão mostra imagem (emoji), nome, preços e botão.
  const grid = document.querySelector('.products-grid');
  if (!grid) return;

  grid.innerHTML = '';
  const items = products.slice(0, 3);

  items.forEach(p => {
    const discountCalc = (p && p.old_price && p.new_price)
      ? Math.max(0, Math.round(100 - (Number(p.new_price) / Number(p.old_price)) * 100))
      : (p && typeof p.discount === 'number' ? p.discount : 0);

    const card = document.createElement('article');
    card.className = 'product-card';
    card.innerHTML = `
      <div class="product-image">
        <span>${escapeHtml(p?.emoji || '🛍️')}</span>
        <div class="discount-badge">-${discountCalc}%</div>
      </div>
      <div class="product-info">
        <h3 class="product-name">${escapeHtml(p?.name || 'Produto')}</h3>
        <div class="price-container">
          <span class="old-price">${formatBRL(p?.old_price)}</span>
          <span class="new-price">${formatBRL(p?.new_price)}</span>
        </div>
        <button class="buy-button">Comprar Agora</button>
      </div>
    `;
    grid.appendChild(card);
  });

  attachBuyButtonHandlers();
}

async function loadProducts() {
  // ---------------------------------
  // Carregamento de produtos (Supabase -> mock)
  // 1) Tenta buscar no Supabase usando as credenciais de index.html
  // 2) Se der erro ou vier vazio, usa uma lista mock para não quebrar a página
  // ---------------------------------

  // Produtos de demonstração (fallback)
  const mockProducts = [
    { name: 'Smartphone Premium', old_price: 3999, new_price: 1199, emoji: '📱' },
    { name: 'Notebook Ultra', old_price: 5999, new_price: 2399, emoji: '💻' },
    { name: 'Fone Bluetooth', old_price: 899, new_price: 314, emoji: '🎧' }
  ];

  // Consultar diretamente do Supabase
  // Explicação:
  // - `window.supabase` vem do SDK carregado no index.html
  // - `createClient(url, anonKey)` cria um cliente para acessar o banco
  // - A consulta usa `.from('products').select('*')` para pegar todos os campos
  // - Ordenamos por `created_at` desc e limitamos a 3 itens mais recentes
  try {
    const { createClient } = window.supabase || {};
    const cfg = window.__SUPABASE || {};
    if (typeof createClient === 'function' && cfg.url && cfg.anonKey) {
      const client = createClient(cfg.url, cfg.anonKey);
      const { data, error } = await client
        .from('products')
        .select('*')
        .order('created_at', { ascending: false })
        .limit(3);

      if (error) throw error;
      if (Array.isArray(data) && data.length) {
        // Se deu certo e veio conteúdo, exibimos os produtos reais
        renderProducts(data);
        return;
      }
    }
  } catch (errSupabase) {
    // Em caso de falha (sem internet, sem RLS, chave inválida...),
    // seguimos para o fallback.
    console.warn('Falha ao consultar Supabase:', errSupabase);
  }

  // Fallback para mock
  // Mostra a lista de demonstração para manter a experiência do aluno.
  renderProducts(mockProducts);
  showToast('Exibindo produtos de demonstração.');
}

document.addEventListener('DOMContentLoaded', () => {
  // Quando o HTML terminar de carregar, iniciamos a busca de produtos.
  loadProducts();
});

// keyframes para toasts
const toastStyle = document.createElement('style');
toastStyle.textContent = `
  @keyframes slideIn {
    from { transform: translateX(400px); opacity: 0; }
    to { transform: translateX(0); opacity: 1; }
  }
  @keyframes slideOut {
    from { transform: translateX(0); opacity: 1; }
    to { transform: translateX(400px); opacity: 0; }
  }
`;
document.head.appendChild(toastStyle);
```

Abrir o supabase e criar a tabela abaixo usando sql editor

```sql
-- Criar extensão para UUID (caso não exista)
CREATE EXTENSION IF NOT EXISTS "uuid-ossp";

-- Criar tabela de produtos
CREATE TABLE public.products (
  id UUID DEFAULT uuid_generate_v4() PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  emoji VARCHAR(10) NOT NULL DEFAULT '📦',
  old_price DECIMAL(10, 2) NOT NULL CHECK (old_price >= 0),
  new_price DECIMAL(10, 2) NOT NULL CHECK (new_price >= 0),
  discount INTEGER NOT NULL CHECK (discount >= 0 AND discount <= 100),
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- Criar índice para melhorar performance
CREATE INDEX idx_products_created_at ON public.products(created_at DESC);

-- Habilitar Row Level Security (RLS)
ALTER TABLE public.products ENABLE ROW LEVEL SECURITY;

-- Criar políticas de segurança
CREATE POLICY "Permitir leitura pública de produtos"
ON public.products FOR SELECT
USING (true);

CREATE POLICY "Permitir inserção pública de produtos"
ON public.products FOR INSERT
WITH CHECK (true);

CREATE POLICY "Permitir atualização pública de produtos"
ON public.products FOR UPDATE
USING (true);

CREATE POLICY "Permitir deleção pública de produtos"
ON public.products FOR DELETE
USING (true);

-- Função para atualizar updated_at automaticamente
CREATE OR REPLACE FUNCTION update_updated_at_column()
RETURNS TRIGGER AS $$
BEGIN
  NEW.updated_at = NOW();
  RETURN NEW;
END;
$$ LANGUAGE plpgsql;

-- Criar trigger para atualizar updated_at
CREATE TRIGGER update_products_updated_at
BEFORE UPDATE ON public.products
FOR EACH ROW
EXECUTE FUNCTION update_updated_at_column();

-- Inserir produtos de exemplo
INSERT INTO public.products (name, emoji, old_price, new_price, discount) VALUES
('Smartphone Premium', '📱', 3999.00, 1199.00, 70),
('Notebook Ultra', '💻', 5999.00, 2399.00, 60),
('Fone Bluetooth', '🎧', 899.00, 314.00, 65);
```

Agora vamos criar a pasta backend

```makefile
/backend
 |_/src
 |	|_/config
 |	| |_supabase.js
 |	|_/controllers
 |	|	|_productController.js
 |	|_/routes
 |	|	|_productRoutes.js
 |	|_/validators
 |	|	|_productValidator.js
 |	|server.js
 |.env
 |package.json
 
```

/backend/src/config   crie o arquivo supabase.js

```jsx
const { createClient } = require('@supabase/supabase-js');

// Validar variáveis de ambiente
if (!process.env.SUPABASE_URL || !process.env.SUPABASE_KEY) {
  console.error('❌ Erro: SUPABASE_URL e SUPABASE_KEY devem estar definidos no .env');
  process.exit(1);
}

// Criar cliente Supabase
const supabase = createClient(
  process.env.SUPABASE_URL,
  process.env.SUPABASE_KEY
);

// Testar conexão
const testConnection = async () => {
  try {
    const { data, error } = await supabase
      .from('products')
      .select('count')
      .limit(1);
    
    if (error) throw error;
    console.log('✅ Supabase conectado com sucesso!');
  } catch (error) {
    console.error('❌ Erro ao conectar Supabase:', error.message);
  }
};

testConnection();

module.exports = supabase;
```

/backend/src/controllers  crie  productController.js

```jsx
const supabase = require('../config/supabase');
const { validateProduct, validateId } = require('../validators/productValidator');

// GET - Listar todos os produtos
exports.getAllProducts = async (req, res) => {
  try {
    const { data, error } = await supabase
      .from('products')
      .select('*')
      .order('created_at', { ascending: false });

    if (error) throw error;

    // Calcular economia para cada produto
    const productsWithSavings = data.map(product => ({
      ...product,
      savings: product.old_price - product.new_price
    }));

    res.status(200).json({
      success: true,
      count: productsWithSavings.length,
      data: productsWithSavings
    });
  } catch (error) {
    res.status(500).json({
      success: false,
      message: 'Erro ao buscar produtos',
      error: error.message
    });
  }
};

// GET - Buscar produto por ID
exports.getProductById = async (req, res) => {
  try {
    const { id } = req.params;

    // Validar ID
    if (!validateId(id)) {
      return res.status(400).json({
        success: false,
        message: 'ID inválido'
      });
    }

    const { data, error } = await supabase
      .from('products')
      .select('*')
      .eq('id', id)
      .single();

    if (error) {
      if (error.code === 'PGRST116') {
        return res.status(404).json({
          success: false,
          message: 'Produto não encontrado'
        });
      }
      throw error;
    }

    // Adicionar economia
    const productWithSavings = {
      ...data,
      savings: data.old_price - data.new_price
    };

    res.status(200).json({
      success: true,
      data: productWithSavings
    });
  } catch (error) {
    res.status(500).json({
      success: false,
      message: 'Erro ao buscar produto',
      error: error.message
    });
  }
};

// POST - Criar novo produto
exports.createProduct = async (req, res) => {
  try {
    // Validar dados
    const validation = validateProduct(req.body);
    if (!validation.isValid) {
      return res.status(400).json({
        success: false,
        message: 'Dados inválidos',
        errors: validation.errors
      });
    }

    const { name, emoji, old_price, new_price, discount } = req.body;

    const { data, error } = await supabase
      .from('products')
      .insert([
        {
          name: name.trim(),
          emoji: emoji.trim(),
          old_price: parseFloat(old_price),
          new_price: parseFloat(new_price),
          discount: parseInt(discount)
        }
      ])
      .select()
      .single();

    if (error) throw error;

    res.status(201).json({
      success: true,
      message: 'Produto criado com sucesso!',
      data: data
    });
  } catch (error) {
    res.status(400).json({
      success: false,
      message: 'Erro ao criar produto',
      error: error.message
    });
  }
};

// PUT - Atualizar produto
exports.updateProduct = async (req, res) => {
  try {
    const { id } = req.params;

    // Validar ID
    if (!validateId(id)) {
      return res.status(400).json({
        success: false,
        message: 'ID inválido'
      });
    }

    // Validar dados (parcial)
    const validation = validateProduct({ ...req.body });
    if (!validation.isValid) {
      return res.status(400).json({
        success: false,
        message: 'Dados inválidos',
        errors: validation.errors
      });
    }

    // Preparar dados para atualização
    const updateData = {};
    if (req.body.name) updateData.name = req.body.name.trim();
    if (req.body.emoji) updateData.emoji = req.body.emoji.trim();
    if (req.body.old_price !== undefined) updateData.old_price = parseFloat(req.body.old_price);
    if (req.body.new_price !== undefined) updateData.new_price = parseFloat(req.body.new_price);
    if (req.body.discount !== undefined) updateData.discount = parseInt(req.body.discount);

    const { data, error } = await supabase
      .from('products')
      .update(updateData)
      .eq('id', id)
      .select()
      .single();

    if (error) {
      if (error.code === 'PGRST116') {
        return res.status(404).json({
          success: false,
          message: 'Produto não encontrado'
        });
      }
      throw error;
    }

    res.status(200).json({
      success: true,
      message: 'Produto atualizado com sucesso!',
      data: data
    });
  } catch (error) {
    res.status(400).json({
      success: false,
      message: 'Erro ao atualizar produto',
      error: error.message
    });
  }
};

// DELETE - Deletar produto
exports.deleteProduct = async (req, res) => {
  try {
    const { id } = req.params;

    // Validar ID
    if (!validateId(id)) {
      return res.status(400).json({
        success: false,
        message: 'ID inválido'
      });
    }

    const { data, error } = await supabase
      .from('products')
      .delete()
      .eq('id', id)
      .select()
      .single();

    if (error) {
      if (error.code === 'PGRST116') {
        return res.status(404).json({
          success: false,
          message: 'Produto não encontrado'
        });
      }
      throw error;
    }

    res.status(200).json({
      success: true,
      message: 'Produto deletado com sucesso!',
      data: data
    });
  } catch (error) {
    res.status(500).json({
      success: false,
      message: 'Erro ao deletar produto',
      error: error.message
    });
  }
};
```

/backend/src/routers  crie o arquivo  productRouters.js

```jsx
const express = require('express');
const router = express.Router();
const productController = require('../controllers/productController');

// Rotas de produtos
router.get('/products', productController.getAllProducts);
router.get('/products/:id', productController.getProductById);
router.post('/products', productController.createProduct);
router.put('/products/:id', productController.updateProduct);
router.delete('/products/:id', productController.deleteProduct);

module.exports = router;
```

/backend/src/validators   crie o arquivo  server.js

```jsx
require('dotenv').config();
const express = require('express');
const cors = require('cors');
const productRoutes = require('./routes/productRoutes');

const app = express();
const PORT = process.env.PORT || 3000;

// Middlewares
app.use(cors()); // Permitir requisições do frontend
app.use(express.json()); // Parsear JSON no body
app.use(express.urlencoded({ extended: true })); // Parsear form data

// Rota de teste
app.get('/', (req, res) => {
  res.json({
    message: '🎉 API Back Friday está funcionando!',
    version: '1.0.0',
    database: 'Supabase (PostgreSQL)',
    endpoints: {
      products: '/api/products'
    }
  });
});

// Rotas da API
app.use('/api', productRoutes);

// Middleware de erro 404
app.use((req, res) => {
  res.status(404).json({
    success: false,
    message: 'Rota não encontrada'
  });
});

// Iniciar servidor
app.listen(PORT, () => {
  console.log(`🚀 Servidor rodando na porta ${PORT}`);
  console.log(`📍 http://localhost:${PORT}`);
});
```

No arquivo .env

```jsx
PORT=3000
SUPABASE_URL=coloqueaquisuaurl
SUPABASE_KEY=coloqueaquisuakey
```
