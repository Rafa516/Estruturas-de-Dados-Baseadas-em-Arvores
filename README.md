# Estruturas-de-Dados-Baseadas-em-Arvores

## O que são Estruturas de Dados em Árvore?
Estruturas de dados baseadas em árvores são modelos hierárquicos que organizam elementos de forma não linear. Elas são amplamente utilizadas para representar relações de hierarquia, otimizar buscas, inserções e remoções, além de permitir operações eficientes em grandes volumes de dados. Exemplos comuns incluem **árvores binárias**, **AVL**, **Red-Black** e **B-Trees**.

---

## Por que B-Trees?
As **B-Trees** (ou Árvores-B) são estruturas especializadas projetadas para funcionar eficientemente em sistemas que lidam com armazenamento secundário (como discos rígidos ou SSDs). Elas minimizam operações de I/O, tornando-as ideais para bancos de dados e sistemas de arquivos. Suas principais características são:
- **Balanceamento automático**: Garante que todos os nós folha estejam no mesmo nível.
- **Alto grau de ramificação**: Cada nó pode conter múltiplas chaves e filhos, reduzindo a altura da árvore.
- **Eficiência em operações**: Busca, inserção e remoção em tempo logarítmico (`O(log n)`).

---

## Estrutura de uma B-Tree
Uma B-Tree de ordem `m` possui as seguintes propriedades:
1. **Ordem**: Define o número máximo de filhos que um nó pode ter.
2. **Nós internos**:
   - Armazenam entre `⌈m/2⌉ - 1` e `m - 1` chaves.
   - Possuem entre `⌈m/2⌉` e `m` filhos.
3. **Nós folha**: Estão sempre no mesmo nível.
4. **Crescimento**: A árvore expande pela raiz, não pelas folhas.

### Exemplo de um Nó em uma B-Tree (ordem 3):
[ [chave1, chave2], [filho1, filho2, filho3] ]


---

## Operações Básicas
### 1. Busca
- Começa na raiz e compara as chaves para decidir em qual subárvore prosseguir.
- Complexidade: `O(log n)`.

### 2. Inserção
- Sempre ocorre em um nó folha.
- Se o nó exceder a capacidade máxima, é feito um **split** (divisão), propagando uma chave para o nó pai.
- Exemplo de split em ordem 3:
 Nó cheio: [10, 20, 30] → Divide em [10], [30] e propaga 20 para o pai.


### 3. Remoção
- Remove a chave do nó folha ou de um nó interno (substituindo pelo predecessor/sucessor).
- Se a remoção violar as regras da B-Tree, ocorre uma **fusão** de nós ou redistribuição de chaves.

---

## Vantagens das B-Trees
- **Eficiência em disco**: Reduz acessos a memória secundária devido à baixa altura.
- **Balanceamento dinâmico**: Não requer reorganizações completas após inserções/remoções.
- **Escalabilidade**: Ideal para grandes conjuntos de dados (ex: índices em bancos de dados).

---

## Aplicações Práticas
1. **Bancos de dados** (ex: MySQL, PostgreSQL usam B-Trees para índices).
2. **Sistemas de arquivos** (ex: NTFS, ext4).
3. **Bancos de dados NoSQL** (ex: MongoDB para índices compostos).
4. **Gestão de memória virtual** em sistemas operacionais.

---

## Exemplo Simples em Código (Pseudocódigo)
```python
class BTreeNode:
  def __init__(self, order):
      self.order = order
      self.keys = []
      self.children = []

def insert(node, key):
  if len(node.keys) == (2 * node.order) - 1:
      new_node = BTreeNode(node.order)
      new_node.children.append(node)
      split_child(new_node, 0)
      insert_non_full(new_node, key)
      return new_node
  else:
      insert_non_full(node, key)
      return node
````
Outras matérias relacionadas:
[PostgreSQL B-Tree Index Explained](https://www.qwertee.io/blog/postgresql-b-tree-index-explained-part-1/)


