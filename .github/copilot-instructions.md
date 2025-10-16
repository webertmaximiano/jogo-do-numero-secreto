# Jogo do Número Secreto - Instruções para Agentes de IA

## Visão Geral da Arquitetura
Este é um jogo de adivinhação simples com interface web que utiliza:
- **Vanilla JavaScript** para lógica de jogo
- **CSS com gradientes e imagens de fundo** para design visual
- **ResponsiveVoice.js** para síntese de voz em português brasileiro
- **Estrutura modular** com funções específicas para cada responsabilidade

## Padrões de Código Específicos

### Gerenciamento de Estado Global
```javascript
let listaDeNumerosSorteados = [];
let numeroLimite = 10;
let numeroSecreto = gerarNumeroAleatorio();
let tentativas = 1;
```
- Use variáveis globais para estado do jogo (não modules/classes)
- `listaDeNumerosSorteados` evita repetição de números até esgotar todas as possibilidades
- `numeroLimite` é configurável (atualmente 1-10)

### Função de Exibição com Áudio
```javascript
function exibirTextoNaTela(tag, texto) {
    let campo = document.querySelector(tag);
    campo.innerHTML = texto;
    responsiveVoice.speak(texto, 'Brazilian Portuguese Female', {rate:1.2});
}
```
- **Sempre** use `exibirTextoNaTela()` para atualizar conteúdo visual
- Todos os textos são automaticamente narrados em português brasileiro
- Rate de 1.2x para velocidade de fala otimizada

### Algoritmo de Números Únicos
A função `gerarNumeroAleatorio()` implementa um padrão específico:
- Verifica se a lista atingiu `numeroLimite` e a reseta
- Usa recursão para garantir números únicos
- **Debug**: `console.log(listaDeNumerosSorteados)` sempre ativo

### Gerenciamento de Botões
- Botão "Novo jogo" inicia **disabled** (`reiniciar.setAttribute('disabled', true)`)
- Habilitado apenas após vitória (`removeAttribute('disabled')`)
- Use `getElementById('reiniciar')` para referência direta

## Convenções de UI/UX

### Layout Responsivo
- Breakpoint principal: `1250px`
- Fontes: `Chakra Petch` (títulos), `Inter` (textos/botões)
- Imagem de pessoa desaparece em telas menores
- Container flexível com `80%` de largura/altura

### Sistema de Cores
- Azul primário: `#1875E8` (texto destacado, botões, bordas)
- Gradiente de fundo: `#1354A5` → `#041832` → `#01080E`
- Input com fundo branco e texto azul

### Estrutura de Mensagens
- H1 para status principal ("Jogo do número secreto", "Acertou!")
- Parágrafo para instruções e feedback
- Pluralização dinâmica: "tentativa" vs "tentativas"

## Fluxo de Desenvolvimento

### Teste Local
- Abrir `index.html` diretamente no navegador
- Não requer servidor web ou build process
- Testar com ResponsiveVoice requer conexão à internet

### Adicionando Recursos
- Imagens em `/img/` (ia.png, code.png, Ruido.png, bg.png)
- Modificar `numeroLimite` para alterar dificuldade
- Personalizar voz alterando parâmetros do ResponsiveVoice

## Integração Externa
- **ResponsiveVoice.js**: CDN obrigatório para funcionalidade de áudio
- **Google Fonts**: Chakra Petch e Inter via CDN
- Sem dependências de build ou package managers