#include <iostream>
#include <vector>
#include <omp.h>

using namespace std;

// Parallel Reduction Operations
void parallelReductionOperations(const vector<int>& arr) {
    int min_val = arr[0];
    int max_val = arr[0];
    int sum = 0;
    int n = arr.size();

    #pragma omp parallel for reduction(min:min_val) reduction(max:max_val) reduction(+:sum)
    for (int i = 0; i < n; ++i) {
        if (arr[i] < min_val) {
            min_val = arr[i];
        }
        if (arr[i] > max_val) {
            max_val = arr[i];
        }
        sum += arr[i];
    }

    double average = static_cast<double>(sum) / n;

    cout << "Minimum: " << min_val << endl;
    cout << "Maximum: " << max_val << endl;
    cout << "Sum: " << sum << endl;
    cout << "Average: " << average << endl;
}

int main() {
    vector<int> arr = {5, 8, 2, 10, 3, 6, 1, 9, 7, 4};
    parallelReductionOperations(arr);
    return 0;
}
