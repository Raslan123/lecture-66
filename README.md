# lecture-66
#include <iostream>
using namespace std;

int partition(int* arr, int start, int end) {
    int pivot = arr[start];
    int count = 0;

    // Count how many elements are less than the pivot
    for (int i = start + 1; i <= end; i++) {
        if (arr[i] < pivot) {
            count++;
        }
    }

    // Find the correct position of the pivot element
    int pivotIndex = start + count;
    swap(arr[pivotIndex], arr[start]);

    // Sort the elements around the pivot
    int i = start, j = end;

    while (i < pivotIndex && j > pivotIndex) {
        while (arr[i] < pivot) {
            i++;
        }

        while (arr[j] > pivot) {
            j--;
        }

        if (i < pivotIndex && j > pivotIndex) {
            swap(arr[i++], arr[j--]);
        }
    }

    return pivotIndex;
}

void quicksort(int* arr, int start, int end) {
    if (start >= end) return;

    int partitionIndex = partition(arr, start, end);

    quicksort(arr, start, partitionIndex - 1);
    quicksort(arr, partitionIndex + 1, end);
}

int main() {
    int arr[] = {5, 1, 3, 10, 7, 14, 2};
    int size = sizeof(arr) / sizeof(arr[0]);

    quicksort(arr, 0, size - 1);

    cout << "Sorted array: ";
    for (int i = 0; i < size; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;

    return 0;
}
