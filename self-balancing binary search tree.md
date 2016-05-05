```
#include<iostream>
#include<vector>
#include<cstdio>
#include<cstring>
#include<map>
#include<cmath>
#include<list>
#include<algorithm>
#include<set>
#include<queue>
#include<string>
#include<stack>
using namespace std;
struct Node{
    int value;
    Node *leftchild;
    Node *rightchild;
    int height;
    Node(int key):value(key),leftchild(NULL),rightchild(NULL),height(0){}
};
int gethight(Node *node){

    if(node==NULL)return -1;
    return node->height;
}
bool isbalanced(Node *node){

    return abs(gethight(node->leftchild)-gethight(node->rightchild))<2;

}
Node *LL(Node *parent){
    Node *child=parent->leftchild;
    parent->leftchild=child->rightchild;
    child->rightchild=parent;

    parent->height=max(gethight(parent->leftchild),gethight(parent->rightchild))+1;
    child->height=max(gethight(child->leftchild),gethight(child->rightchild))+1;

    return child;
}
Node *RR(Node *parent){
    Node *child=parent->rightchild;
    parent->rightchild=child->leftchild;
    child->leftchild=parent;

    parent->height=max(gethight(parent->leftchild),gethight(parent->rightchild))+1;
    child->height=max(gethight(child->leftchild),gethight(child->rightchild))+1;

    return child;
}
Node *LR(Node *parent){
    Node *child=parent->leftchild;
    parent->leftchild=RR(child);

    return LL(parent);
}
Node *RL(Node *parent){
    Node *child=parent->rightchild;
    parent->rightchild=LL(child);

    return RR(parent);
}
Node *insertnode(Node *root,int newvalue){

    if(root!=NULL){

        if(newvalue>root->value){
            root->rightchild=insertnode(root->rightchild,newvalue);
            if(!isbalanced(root)){
                if(newvalue>root->rightchild->value)
                    root=RR(root);
                else
                    root=RL(root);
            }
        }

        else {
            root->leftchild=insertnode(root->leftchild,newvalue);
            if(!isbalanced(root)){
                if(newvalue>root->leftchild->value)
                    root=LR(root);
                else
                    root=LL(root);
            }


        }
    }
    else
    root=new Node(newvalue);

    root->height=max(gethight(root->leftchild),gethight(root->rightchild))+1;

    return root;
}


int main(){
    int n;
    scanf("%d",&n);

    Node *root=NULL;

    while(n--){
        int x;
        scanf("%d",&x);
        root=insertnode(root,x);
    }

    printf("%d\n",root->value);

    return 0;
}
```
