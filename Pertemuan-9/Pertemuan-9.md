# Pertemuan 9
## tugas 1
cat << 'EOF' > $HOME/praktikum-os/week09/scripts/absensi.sh
#!/bin/bash

LOG_DIR="../logs"
TANGGAL=$(date "+%Y-%m-%d")
FILE_ABSENSI="$LOG_DIR/absensi-$TANGGAL.txt"

show_help() {
    echo "Penggunaan: ./absensi.sh [OPSI] [NAMA STATUS]"
    echo "Opsi:"
    echo "  -h          Menampilkan bantuan ini"
    echo "  -r          Menampilkan rekapitulasi jumlah status"
    echo ""
    echo "Contoh: ./absensi.sh \"Budi Santoso\" hadir"
}

show_recap() {
    if [ ! -f "$FILE_ABSENSI" ]; then
        echo "Belum ada data absensi untuk hari ini ($TANGGAL)."
        exit 0
    fi

    echo "=== Rekapitulasi Absensi $TANGGAL ==="
    for status in hadir izin alpha; do
        # Menghitung jumlah kata status secara spesifik (case-insensitive)
        count=$(grep -io " - $status" "$FILE_ABSENSI" | wc -l)
        echo "$status: $count"
    done
}

while getopts "hr" opt; do
  case ${opt} in
    h ) show_help; exit 0 ;;
    r ) show_recap; exit 0 ;;
    \? ) show_help; exit 1 ;;
  esac
done

shift $((OPTIND -1))

if [ $# -lt 2 ]; then
    echo "Error: Argumen kurang lengkap."
    show_help
    exit 1
fi

NAMA=$1
STATUS=$(echo "$2" | tr '[:upper:]' '[:lower:]')
JAM=$(date "+%H:%M")

if [[ "$STATUS" =~ ^(hadir|izin|alpha)$ ]]; then
    echo "[$JAM] $NAMA - $STATUS" >> "$FILE_ABSENSI"
    echo "Berhasil mencatat: $NAMA sebagai $STATUS"
else
    echo "Error: Status harus 'hadir', 'izin', atau 'alpha'."
    exit 1
fi
EOF
<img width="706" height="532" alt="image" src="https://github.com/user-attachments/assets/e8fc121a-8fc7-425e-a59a-eb9ab0750c66" />

## Tugas 2
cat << 'EOF' > $HOME/praktikum-os/week09/scripts/healthcheck.sh
#!/bin/bash

set -euo pipefail

LOG_DIR="../logs"
TANGGAL=$(date "+%Y-%m-%d")
LOG_FILE="$LOG_DIR/healthcheck-$TANGGAL.log"
THRESHOLD=80

trap "echo 'Pemeriksaan dibatalkan'; exit" SIGINT SIGTERM

print_header() {
    local title=$1
    echo -e "\n=== $title ==="
}

show_usage() {
    echo "Penggunaan: bash healthcheck.sh [-t threshold]"
    echo "  -t: Set batas peringatan penggunaan disk (default: 80)"
    exit 1
}

while getopts "t:h" opt; do
  case ${opt} in
    t ) THRESHOLD=$OPTARG ;;
    h ) show_usage ;;
    \? ) show_usage ;;
  esac
done

perform_check() {
    print_header "INFORMASI SISTEM"
    echo "Waktu    : $(date)"
    echo "Hostname : $(hostname)"
    echo "Uptime   : $(uptime -p)"

    print_header "PENGGUNAAN MEMORI"
    free -h

    print_header "PENGGUNAAN DISK & PERINGATAN"
    # Menampilkan disk dan cek threshold
    df -h | grep '^/' | while read -r line; do
        usage=$(echo "$line" | awk '{print $5}' | sed 's/%//')
        filesystem=$(echo "$line" | awk '{print $1}')
        
        echo "$line"
        
        if [ "$usage" -gt "$THRESHOLD" ]; then
            echo ">>> PERINGATAN: Filesystem $filesystem sudah mencapai ${usage}%! (Batas: ${THRESHOLD}%)"
        fi
    done
}
mkdir -p "$LOG_DIR"

{
    print_header "LAPORAN HEALTH CHECK"
    perform_check
} | tee -a "$LOG_FILE"

EOF
<img width="797" height="437" alt="image" src="https://github.com/user-attachments/assets/06d5eca2-aa27-42ca-81d2-996e85a1263c" />
<img width="791" height="479" alt="image" src="https://github.com/user-attachments/assets/3213564a-ca28-4d9b-8d00-299f96174fd1" />
<img width="887" height="857" alt="image" src="https://github.com/user-attachments/assets/2b9d3212-14a1-4042-af17-b39ca8ad721e" />

