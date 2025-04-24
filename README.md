# ks
Desenvolvimento da Aplicação no Git Codespaces
#include <iostream>
#include <vector>
using namespace std;

int sumVector(const vector<int>& numbers) {
    int sum = 0;
    for (int num : numbers) {
        sum += num;
    }
    return sum;
}

int main() {
    vector<int> numbers = {5, 10, 15, 20};
    cout << "A soma dos números é: " << sumVector(numbers) << endl;
    return 0;
}
