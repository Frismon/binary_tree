class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None


def preorder(node):
    """Прямий обхід (Preorder Traversal)"""
    if node is None:
        return
    print(node.data, end=' ')
    preorder(node.left)
    preorder(node.right)


def inorder(node):
    """Внутрішній обхід (Inorder Traversal)"""
    if node is None:
        return
    inorder(node.left)
    print(node.data, end=' ')
    inorder(node.right)


def postorder(node):
    """Зворотний обхід (Postorder Traversal)"""
    if node is None:
        return
    postorder(node.left)
    postorder(node.right)
    print(node.data, end=' ')


def build_tree(edges_left, edges_right):
    nodes = {}

    # Створюємо вузли та зв'язки
    for parent, child in edges_left + edges_right:
        if parent not in nodes:
            nodes[parent] = Node(parent)
        if child not in nodes:
            nodes[child] = Node(child)

        # Налаштовуємо ліві та праві піддерева
        if (parent, child) in edges_left:
            nodes[parent].left = nodes[child]
        elif (parent, child) in edges_right:
            nodes[parent].right = nodes[child]

    # Знаходимо корінь дерева
    root = next((node for node in nodes.values() if node.data == list(edges_left[0])[0]), None)
    return root


def main():
    # Припустимо, користувач вводить ребра у вигляді тексту
    L_input = input("Введіть L ребра (формат 'parent,child') розділені комою: ")
    R_input = input("Введіть R ребра (формат 'parent,child') розділені комою: ")

    # Перетворення введення у списки кортежів
    edges_left = [tuple(edge.split(',')) for edge in L_input.split(';')]
    edges_right = [tuple(edge.split(',')) for edge in R_input.split(';')]

    # Побудова дерева
    root = build_tree(edges_left, edges_right)

    # Виклик функцій для обходу
    print("Прямий обхід (Preorder Traversal):")
    preorder(root)
    print("\nВнутрішній обхід (Inorder Traversal):")
    inorder(root)
    print("\nЗворотний обхід (Postorder Traversal):")
    postorder(root)


if __name__ == '__main__':
    main()
