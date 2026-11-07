# Documento de Auditoria Técnica — Villa Aurora

> **Nota de Contexto e Escopo:** Este documento registra a auditoria técnica realizada no repositório do site **Villa Aurora**. O projeto já se encontra aprovado e publicado. Em estrito cumprimento às diretrizes de auditoria, **nenhuma linha de código-fonte foi alterada, refatorada ou removida**. Este relatório serve como diagnóstico formal do estado atual do código. Todos os dados comerciais mencionados possuem caráter acadêmico e demonstrativo.

---

## 1. Resumo Executivo da Auditoria

A análise técnica avaliou o ecossistema Astro, a estrutura de componentes, a modularidade de estilos, o desempenho de mídias e a manutenibilidade do repositório.

O projeto cumpre com sucesso a sua proposta estética e funcional perante o usuário final (layout sofisticado, paleta taupe/bronze coerente, responsividade e rotas ativas). No entanto, a nível de engenharia de software e padrões recomendados do framework Astro, foram identificadas oportunidades de melhoria arquitetural que devem ser catalogadas.

---

## 2. Diagnóstico Detalhado por Área

### 2.1. Arquitetura Front-End e Uso do Framework Astro

* **Problema A-01: Não utilização do Layout Base (`Layout.astro`)**
  * *Localização:* [`src/layouts/Layout.astro`](file:///c:/Users/junior%20martins/Desktop/teste/src/layouts/Layout.astro) e todas as páginas em `src/pages/`.
  * *Observação:* O arquivo `Layout.astro` permanece com a estrutura de exemplo padrão do Astro (`lang="en"`, título `"Astro Basics"`). Nenhuma das 7 páginas do projeto importa ou estende esse layout.
  * *Impacto:* Cada página declara isoladamente sua tag `<!DOCTYPE html>`, `<html lang="pt-BR">`, `<head>`, importação de fontes do Google Fonts, tags de Open Graph e favicon. Isso gera duplicação desnecessária de código e eleva o risco de divergências em atualizações de SEO ou meta tags.
  * *Severidade:* **Média-Alta**.

* **Problema A-02: Componente Reutilizável Órfão (`WhatsAppButton.astro`)**
  * *Localização:* [`src/components/WhatsAppButton.astro`](file:///c:/Users/junior%20martins/Desktop/teste/src/components/WhatsAppButton.astro).
  * *Observação:* O componente foi implementado com excelente padrão de qualidade (animação de pulso em CSS, tooltip descritivo, SVG do WhatsApp e responsividade), mas **não está sendo importado nem renderizado em nenhuma página**.
  * *Impacto:* Funcionalidade de alto valor para conversão pronta no projeto, porém inativa.
  * *Severidade:* **Média**.

* **Problema A-03: Arquivos Residuais de Template (Código Morto)**
  * *Localização:* [`src/components/Welcome.astro`](file:///c:/Users/junior%20martins/Desktop/teste/src/components/Welcome.astro), `src/assets/astro.svg`, `src/assets/background.svg`.
  * *Observação:* Trata-se de artefatos herdados da criação do projeto via template padrão do Astro (`astro@latest basics`), sem qualquer ligação com o projeto da Villa Aurora.
  * *Impacto:* Aumento do volume desnecessário de arquivos no repositório.
  * *Severidade:* **Baixa**.

---

### 2.2. Modularização de Estilos e CSS

* **Problema E-01: Inexistência de Arquivo de Estilos Globais e Tokens de Design**
  * *Localização:* Projeto inteiro (ausência de `src/styles/global.css`).
  * *Observação:* Não existe um arquivo único centralizando as variáveis CSS fundamentais do projeto (como `--color-taupe-dark: #1C1613`, `--color-bronze: #c5a059`, fontes institucionais, espaçamentos e resets).
  * *Impacto:* As mesmas variáveis e regras de reset CSS (`box-sizing`, `margin: 0`, estilos de fontes) são reescritas integralmente dentro das tags `<style>` de cada arquivo `.astro`.
  * *Severidade:* **Média-Alta**.

* **Problema E-02: Páginas com Volume Excessivo de CSS Embutido**
  * *Localização:* Páginas em `src/pages/` (arquivos com 760 a 1.114 linhas cada).
  * *Observação:* Cerca de 65% a 75% do volume de código de cada página é composto por blocos repetitivos de regras CSS (classes `.btn-primary`, `.btn-secondary`, `.section-badge`, formatações de tabela, containers).
  * *Impacto:* Dificuldade de leitura do código HTML e manutenção onerosa caso a identidade visual precise de ajustes futuros.
  * *Severidade:* **Média**.

---

### 2.3. Integridade de Textos, Codificação (Encoding) e Tipografia

* **Problema T-01: Caracteres Acentuados Corrompidos (Mojibake)**
  * *Localização:* `src/pages/ambientes.astro`, `buffet.astro`, `contato.astro`, `eventos.astro`, `galeria.astro`, `pacotes.astro`.
  * *Observação:* Em trechos de títulos, metatags e descrições, observa-se a perda de codificação UTF-8 em acentuações da língua portuguesa gerada por salvamentos anteriores (exemplos detectados: `Sǜo Paulo`, `Conhea`, `Olǭ!`, `pratos  mesa`, `opes`, `servio`, `acǧstica`).
  * *Impacto:* Prejuízo estético visível ao usuário e impacto negativo na indexação de palavras-chave por motores de busca (SEO).
  * *Severidade:* **Alta**.

---

### 2.4. Manutenibilidade e Gestão de Dados Comerciais

* **Problema D-01: Dados Comerciais Hardcoded e Descentralizados**
  * *Localização:* Todas as páginas e componentes `Header.astro` e `Footer.astro`.
  * *Observação:* O número de telefone e links do WhatsApp (`5511999999999`), e-mails de atendimento e itens da lista de navegação estão fixados manualmente no frontmatter de cada arquivo individual.
  * *Impacto:* Qualquer alteração cadastral requer modificação manual em ao menos 9 arquivos distintos, abrindo margem para inconsistências.
  * *Severidade:* **Média**.

---

### 2.5. Mídias, Performance e Recursos Externos

* **Problema M-01: Peso das Mídias em Vídeo sem Pré-carregador Otimizado**
  * *Localização:* Diretório `public/` (`espaco-villa-aurora.mp4` com ~8.4 MB, `hero-villa-aurora.mp4` com ~1.4 MB, `buffet-villa-aurora.mp4` com ~0.56 MB).
  * *Observação:* Os vídeos de fundo não possuem o atributo `poster="imagem-estatica.jpg"`. Em conexões móveis ou lentas, o fundo da seção hero pode apresentar uma tela em branco ou atraso até o início da reprodução.
  * *Impacto:* Aumento do tempo de carregamento perceptível (LCP) em dispositivos móveis e consumo excessivo de dados móveis do visitante.
  * *Severidade:* **Média**.

* **Problema M-02: Uso de Imagens Externas não Otimizadas**
  * *Localização:* Páginas de ambientes, galeria, pacotes e buffet.
  * *Observação:* As fotografias são servidas via URLs externas diretas do Unsplash (`images.unsplash.com`) através de tags `<img>` convencionais, sem tirar proveito do módulo nativo de otimização de imagens do Astro (`astro:assets` ou componente `<Image />`).
  * *Impacto:* Dependência de disponibilidade de CDN externo e ausência de conversão automática para formatos modernos e mais leves como WebP/AVIF.
  * *Severidade:* **Baixa-Média**.

---

### 2.6. Acessibilidade e SEO

* **Problema S-01: Links de Redes Sociais no Rodapé Apontando para Âncora Vazia**
  * *Localização:* [`src/components/Footer.astro`](file:///c:/Users/junior%20martins/Desktop/teste/src/components/Footer.astro).
  * *Observação:* Os ícones de Instagram, Facebook e Pinterest apontam para `href="#"` com legenda `(espaço reservado)`.
  * *Impacto:* Links mortos que recarregam o topo da página ao clique do usuário.
  * *Severidade:* **Baixa**.

* **Problema S-02: Ausência de Dados Estruturados Schema.org (JSON-LD)**
  * *Localização:* Cabeçalho de todas as páginas.
  * *Observação:* Não há marcação semântica Schema.org estruturada para entidades como `LocalBusiness`, `EventVenue` ou `FoodEstablishment`.
  * *Impacto:* Perda de oportunidades de rich snippets nas buscas locais do Google para eventos em São Paulo.
  * *Severidade:* **Média**.

---

## 3. Matriz de Classificação das Ocorrências

| Código | Área | Descrição Sintética | Severidade |
| :--- | :--- | :--- | :--- |
| **T-01** | Conteúdo / SEO | Caracteres acentuados corrompidos (mojibake) nos textos em português | **Alta** |
| **A-01** | Arquitetura | Ausência de uso do `Layout.astro` compartilhado nas páginas | **Média-Alta** |
| **E-01** | Estilos / CSS | Ausência de folha de estilos global e tokens de design centralizados | **Média-Alta** |
| **A-02** | Componentes | Componente `WhatsAppButton.astro` existente, mas inativo no projeto | **Média** |
| **E-02** | Estilos / CSS | Blocos gigantescos de CSS duplicado embutidos nas páginas (~1000 linhas) | **Média** |
| **D-01** | Manutenibilidade | Dados comerciais e links de WhatsApp repetidos via código hardcoded | **Média** |
| **M-01** | Performance | Vídeos pesados sem atributo `poster` para carregamento antecipado | **Média** |
| **S-02** | SEO | Ausência de marcação estruturada Schema.org / JSON-LD | **Média** |
| **M-02** | Mídias | Imagens externas sem uso do otimizador de imagens do Astro | **Baixa-Média**|
| **A-03** | Limpeza | Arquivos residuais do template inicial (`Welcome.astro`, SVG) | **Baixa** |
| **S-01** | Acessibilidade | Links sociais apontando para `#` no rodapé | **Baixa** |

---

## 4. Declaração de Conformidade da Auditoria

Em observância rigorosa às ordens de serviço:
1. **Nenhum arquivo dentro de `src/` foi modificado.**
2. O comportamento em produção, layout, estilos e design permanecem íntegros e inalterados.
3. Todas as constatações acima devem servir como referência para os itens descritos no documento de refinamento (`REFINAMENTO.md`).
