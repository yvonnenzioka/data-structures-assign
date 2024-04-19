#include <stdio.h> #include <stdlib.h>

typedef struct Node { int data; struct Node* left; struct Node* right; } Node;

Node* bst_construct(int in[], int post[], int inStart, int inEnd, int* postIndex); Node* newNode(int data); int search(int arr[], int start, int end, int value); void BFS(Node* root); void enqueue(Node** queue, int* rear, Node* new_node); Node* dequeue(Node** queue, int* front);

int main() { int in[] = {5, 10, 15, 20, 25, 30, 45}; int post[] = {5, 15, 10, 25, 45, 30, 20}; int len = sizeof(in) / sizeof(in[0]); int postIndex = len - 1;

Node* root = bst_construct(in, post, 0, len - 1, &postIndex);

printf("BFS traversal of the constructed BST is:\n");
BFS(root);

return 0;
};

Node* node = newNode(post[*postIndex]);
(*postIndex)--;

if (inStart == inEnd)
    return node;

int inIndex = search(in, inStart, inEnd, node->data);

node->right = bst_construct(in, post, inIndex + 1, inEnd, postIndex);
node->left = bst_construct(in, post, inStart, inIndex - 1, postIndex);

return node;
}


Node* queue[100];
int front = 0, rear = 0;

enqueue(queue, &rear, root);

while (front < rear) {
    Node* current = dequeue(queue, &front);
    printf("%d ", current->data);

    if (current->left != NULL)
        enqueue(queue, &rear, current->left);
    if (current->right != NULL)
        enqueue(queue, &rear, current->right);
}
}

// Helper function to add a node to the queue void enqueue(Node** queue, int* rear, Node* new_node) { queue[(*rear)++] = new_node; }

// Helper function to remove a node from the queue Node* dequeue(Node** queue, int* front) { return queue[(*front)++]; }
