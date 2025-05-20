# Penjelasan kode Lower Bound

// Mendeklarasikan metode yang mencari lower bound dari target dalam array yang terurut.
public static int lowerBound(int[] arr, int target) {
int low = 0; // Inisialisasi batas bawah pencarian, mulai dari indeks pertama.
int high = arr.length - 1; // Inisialisasi batas atas pencarian, mulai dari indeks terakhir.
int result = -1; // Variabel untuk menyimpan hasil pencarian, awalnya diset ke -1 (belum ditemukan).

    while (low <= high) { // Selama batas bawah tidak melebihi batas atas, maka akan melanjutkan pencarian.
        int mid = low + (high - low) / 2; // Menentukan indeks tengah untuk membagi pencarian menjadi dua bagian.

        if (arr[mid] == target) { // Jika elemen tengah sama dengan target...
            result = mid; // Simpan indeks sebagai kemungkinan lower bound.
            high = mid - 1; // Melanjutkan pencarian ke kiri untuk menemukan indeks pertama dari elemen tersebut.
        } else if (arr[mid] > target) { // Jika elemen tengah lebih besar dari target...
            high = mid - 1; // Pindahkan batas atas ke kiri karena target pasti ada di bagian kiri array.
        } else { // Jika elemen tengah lebih kecil dari target...
            low = mid + 1; // Pindahkan batas bawah ke kanan karena target pasti ada di bagian kanan array.
        }
    }

    return result; // Mengembalikan hasil pencarian (indeks pertama target), atau -1 jika tidak ditemukan.

}

# Penjelasan kode Upper Bound

// Mendeklarasikan metode yang mencari upper bound dari target dalam array yang terurut.
public static int upperBound(int[] arr, int target) {
int low = 0; // Inisialisasi batas bawah pencarian, mulai dari indeks pertama.
int high = arr.length - 1; // Inisialisasi batas atas pencarian, mulai dari indeks terakhir.
int result = -1; // Variabel untuk menyimpan hasil pencarian, awalnya diset ke -1 (belum ditemukan).

    while (low <= high) { // Selama batas bawah tidak melebihi batas atas, maka akan melanjutkan pencarian.
        int mid = low + (high - low) / 2; // Menentukan indeks tengah untuk membagi pencarian menjadi dua bagian.

        if (arr[mid] == target) { // Jika elemen tengah sama dengan target...
            result = mid; // Simpan indeks sebagai kemungkinan upper bound.
            low = mid + 1; // Lanjutkan pencarian ke kanan untuk menemukan indeks terakhir dari elemen tersebut.
        } else if (arr[mid] > target) { // Jika elemen tengah lebih besar dari target...
            high = mid - 1; // Pindahkan batas atas ke kiri karena target pasti ada di bagian kiri array.
        } else { // Jika elemen tengah lebih kecil dari target...
            low = mid + 1; // Pindahkan batas bawah ke kanan karena target pasti ada di bagian kanan array.
        }
    }

    return result; // Mengembalikan hasil pencarian (indeks terakhir target), atau -1 jika tidak ditemukan.

}

# Penjelasan kode Mencari Elemen Terdekat

// Metode untuk mencari elemen terdekat dengan target dalam array yang terurut.
public static int nearestElement(int[] arr, int target) {
// Inisialisasi batas bawah pencarian.
int low = 0;
// Inisialisasi batas atas pencarian.
int high = arr.length - 1;

    // jika target lebih kecil dari elemen pertama, kembalikan indeks pertama.
    if (target <= arr[0]) {
        return 0;
    }
    // jika target lebih besar dari elemen terakhir, kembalikan indeks terakhir.
    if (target >= arr[high]) {
        return high;
    }

    // Binary search untuk menemukan elemen yang paling dekat dengan target.
    while (low <= high) { // Selama batas bawah tidak melebihi batas atas, maka akan melanjutkan pencarian.
        int mid = low + (high - low) / 2; // Menentukan indeks tengah untuk membagi pencarian menjadi dua bagian.

        if (arr[mid] == target) { // Jika elemen tengah sama dengan target...
            return mid; // Kembalikan indeksnya karena sudah ditemukan.
        }

        if (arr[mid] > target) { // Jika elemen tengah lebih besar dari target...
            high = mid - 1; // Pindahkan batas atas ke kiri karena target ada di bagian kiri array.
        } else { // Jika elemen tengah lebih kecil dari target...
            low = mid + 1; // Pindahkan batas bawah ke kanan karena target ada di bagian kanan array.
        }
    }

    // Setelah binary search berakhir, low > high.
    // Bandingkan arr[high] dan arr[low] untuk melihat mana yang lebih dekat ke target.
    if (Math.abs(arr[high] - target) <= Math.abs(arr[low] - target)) { // Jika elemen di indeks high lebih dekat...
        return high; // Kembalikan indeks high.
    } else { // Jika elemen di indeks low lebih dekat...
        return low; // Kembalikan indeks low.
    }

}

# Penjelasan kode Binary Search pada Array Rotasi

// Metode untuk mencari elemen target dalam array yang telah diputar.
public static int searchInRotatedArray(int[] arr, int target) {
int low = 0; // Inisialisasi batas bawah pencarian.
int high = arr.length - 1; // Inisialisasi batas atas pencarian.

    while (low <= high) { // Selama batas bawah tidak melebihi batas atas, maka akan melanjutkan pencarian.
        int mid = low + (high - low) / 2; // Menentukan indeks tengah untuk membagi pencarian menjadi dua bagian.

        if (arr[mid] == target) { // Jika elemen tengah sama dengan target...
            return mid; // Kembalikan indeksnya karena sudah ditemukan.
        }

        // Periksa apakah bagian kiri terurut
        if (arr[low] <= arr[mid]) { // Jika elemen pertama dalam bagian ini lebih kecil atau sama dengan elemen tengah, maka bagian kiri terurut.
            // Periksa apakah target berada di bagian  kiri yang terurut
            if (arr[low] <= target && target < arr[mid]) { // Jika target berada dalam rentang bagian kiri yang terurut...
                high = mid - 1; // Pindahkan batas atas ke kiri untuk mencari di bagian kiri.
            } else { // Jika target tidak berada dalam rentang bagian kiri yang terurut...
                low = mid + 1; // Pindahkan batas bawah ke kanan untuk mencari di bagian kanan.
            }
        }
        // Setengah kanan terurut
        else { // Jika bagian kiri tidak terurut, maka bagian kanan pasti terurut.
            // Periksa apakah target berada di setengah kanan yang terurut
            if (arr[mid] < target && target <= arr[high]) { // Jika target berada dalam rentang bagian kanan yang terurut...
                low = mid + 1; // Pindahkan batas bawah ke kanan untuk mencari di bagian kanan.
            } else { // Jika target tidak berada dalam rentang bagian kanan yang terurut...
                high = mid - 1; // Pindahkan batas atas ke kiri untuk mencari di bagian kiri.
            }
        }
    }

    return -1; // Jika target tidak ditemukan dalam array, kembalikan -1.

}
