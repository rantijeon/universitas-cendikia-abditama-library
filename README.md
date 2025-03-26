<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Perpustakaan</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 20px; }
        table { width: 100%; border-collapse: collapse; margin-top: 20px; }
        th, td { border: 1px solid black; padding: 8px; text-align: left; }
        th { background-color: #f4f4f4; }
        button { margin-right: 5px; }
    </style>
</head>
<body>
    <h2>Formulir Peminjaman Buku</h2>
    <form id="libraryForm">
        Nama: <input type="text" id="nama" required><br><br>
        NIM: <input type="text" id="nim" required><br><br>
        Tanggal: <input type="date" id="tanggal" required><br><br>
        Program Studi: <input type="text" id="prodi" required><br><br>
        Keperluan: <input type="text" id="keperluan" required><br><br>
        <button type="button" onclick="addEntry()">Tambah</button>
    </form>
    
    <h2>Data Peminjaman</h2>
    <table>
        <thead>
            <tr>
                <th>Nama</th>
                <th>NIM</th>
                <th>Tanggal</th>
                <th>Program Studi</th>
                <th>Keperluan</th>
                <th>Aksi</th>
            </tr>
        </thead>
        <tbody id="dataBody"></tbody>
    </table>
    
    <script>
        function addEntry() {
            let nama = document.getElementById("nama").value;
            let nim = document.getElementById("nim").value;
            let tanggal = document.getElementById("tanggal").value;
            let prodi = document.getElementById("prodi").value;
            let keperluan = document.getElementById("keperluan").value;
            
            if (nama && nim && tanggal && prodi && keperluan) {
                let table = document.getElementById("dataBody");
                let row = table.insertRow();
                row.insertCell(0).innerText = nama;
                row.insertCell(1).innerText = nim;
                row.insertCell(2).innerText = tanggal;
                row.insertCell(3).innerText = prodi;
                row.insertCell(4).innerText = keperluan;
                let actions = row.insertCell(5);
                
                let editButton = document.createElement("button");
                editButton.innerText = "Edit";
                editButton.onclick = function() { editEntry(row); };
                actions.appendChild(editButton);
                
                let deleteButton = document.createElement("button");
                deleteButton.innerText = "Hapus";
                deleteButton.onclick = function() { table.deleteRow(row.rowIndex - 1); };
                actions.appendChild(deleteButton);
                
                document.getElementById("libraryForm").reset();
            } else {
                alert("Semua field harus diisi!");
            }
        }

        function editEntry(row) {
            document.getElementById("nama").value = row.cells[0].innerText;
            document.getElementById("nim").value = row.cells[1].innerText;
            document.getElementById("tanggal").value = row.cells[2].innerText;
            document.getElementById("prodi").value = row.cells[3].innerText;
            document.getElementById("keperluan").value = row.cells[4].innerText;
            row.remove();
        }
    </script>
</body>
</html>
