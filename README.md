<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gunung di Jawa Timur</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Arial', sans-serif;
            line-height: 1.6;
            color: #333;
            background: linear-gradient(135deg, #74b9ff 0%, #0984e3 100%);
            min-height: 100vh;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        header {
            text-align: center;
            color: white;
            margin-bottom: 40px;
        }

        h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }

        .subtitle {
            font-size: 1.2em;
            opacity: 0.9;
        }

        .search-box {
            max-width: 500px;
            margin: 0 auto 40px;
            position: relative;
        }

        .search-box input {
            width: 100%;
            padding: 15px 20px;
            border: none;
            border-radius: 50px;
            font-size: 16px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
            outline: none;
        }

        .gunung-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
            gap: 25px;
            margin-bottom: 40px;
        }

        .gunung-card {
            background: white;
            border-radius: 20px;
            padding: 25px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            opacity: 1;
        }

        .gunung-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 20px 40px rgba(0,0,0,0.3);
        }

        .gunung-card.hidden {
            display: none;
        }

        .gunung-name {
            font-size: 1.5em;
            font-weight: bold;
            color: #2d3436;
            margin-bottom: 10px;
        }

        .gunung-height {
            background: #00b894;
            color: white;
            padding: 8px 15px;
            border-radius: 20px;
            font-weight: bold;
            display: inline-block;
            margin-bottom: 15px;
        }

        .detail-list {
            list-style: none;
        }

        .detail-list li {
            padding: 5px 0;
            border-bottom: 1px solid #eee;
        }

        .detail-list li:last-child {
            border-bottom: none;
        }

        .detail-label {
            font-weight: bold;
            color: #636e72;
        }

        .status {
            padding: 5px 12px;
            border-radius: 15px;
            font-size: 0.9em;
            font-weight: bold;
            margin-top: 10px;
        }

        .status.aktif {
            background: #00b894;
            color: white;
        }

        .status.tidur {
            background: #fdcb6e;
            color: #2d3436;
        }

        footer {
            text-align: center;
            color: white;
            margin-top: 50px;
            padding: 20px;
            opacity: 0.8;
        }

        @media (max-width: 768px) {
            h1 {
                font-size: 2em;
            }
            
            .gunung-grid {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>🏔️ Gunung di Jawa Timur</h1>
            <p class="subtitle">Daftar Gunung Aktif dan Tidur Tertinggi di Jawa Timur</p>
        </header>

        <div class="search-box">
            <input type="text" id="searchInput" placeholder="Cari gunung... (contoh: Semeru, Bromo)">
        </div>

        <div class="gunung-grid" id="gunungGrid">
            <!-- Data akan dimuat oleh JavaScript -->
        </div>

        <footer>
            <p>&copy; 2024 Data Gunung Jawa Timur. Dibuat dengan ❤️ untuk pecinta alam.</p>
        </footer>
    </div>

    <script>
        const gunungData = [
            {
                nama: "Gunung Semeru",
                ketinggian: "3676 mdpl",
                lokasi: "Kab. Malang & Lumajang",
                status: "Aktif",
                tipe: "Stratovolcano",
                deskripsi: "Gunung tertinggi di Pulau Jawa dan gunung berapi paling aktif di Jawa Timur."
            },
            {
                nama: "Gunung Bromo",
                ketinggian: "2392 mdpl",
                lokasi: "Kab. Probolinggo, Pasuruan, & Malang",
                status: "Aktif",
                tipe: "Stratovolcano",
                deskripsi: "Terkenal dengan kaldera laut pasirnya yang luas dan pemandangan matahari terbit spektakuler."
            },
            {
                nama: "Gunung Arjuno",
                ketinggian: "3338 mdpl",
                lokasi: "Kab. Malang & Pasuruan",
                status: "Tidur",
                tipe: "Stratovolcano",
                deskripsi: "Bagian dari kompleks gunung kembar Arjuno-Welirang dengan panorama hutan pinus indah."
            },
            {
                nama: "Gunung Welirang",
                ketinggian: "3156 mdpl",
                lokasi: "Kab. Pasuruan & Malang",
                status: "Aktif",
                tipe: "Stratovolcano",
                deskripsi: "Kawah belerangnya yang aktif dan pemandangan kawah Ratu yang eksotis."
            },
            {
                nama: "Gunung Tengger",
                ketinggian: "2847 mdpl",
                lokasi: "Kab. Probolinggo & Pasuruan",
                status: "Tidur",
                tipe: "Caldera",
                deskripsi: "Caldera terbesar di Jawa Timur yang mengelilingi 5 gunung kecil (Bromo, Batok, dll)."
            },
            {
                nama: "Gunung Iyang-Argapura",
                ketinggian: "3088 mdpl",
                lokasi: "Kab. Probolinggo",
                status: "Tidur",
                tipe: "Stratovolcano",
                deskripsi: "Kompleks gunung kembar tertinggi di Probolinggo dengan jalur pendakian menantang."
            },
            {
                nama: "Gunung Kelud",
                ketinggian: "1731 mdpl",
                lokasi: "Kab. Kediri & Blitar",
                status: "Aktif",
                tipe: "Stratovolcano",
                deskripsi: "Terkenal dengan letusan dahsyat tahun 2014 dan danau kawah yang indah."
            },
            {
                nama: "Gunung Penanggungan",
                ketinggian: "1653 mdpl",
                lokasi: "Kab. Mojokerto & Pasuruan",
                status: "Tidur",
                tipe: "Stratovolcano",
                deskripsi: "Gunung suci dengan banyak situs keramat dan pemandangan Majapahit."
            }
        ];

        function renderGunung() {
            const searchTerm = document.getElementById('searchInput').value.toLowerCase();
            const gunungGrid = document.getElementById('gunungGrid');
            
            gunungGrid.innerHTML = gunungData
                .filter(gunung => 
                    gunung.nama.toLowerCase().includes(searchTerm) ||
                    gunung.lokasi.toLowerCase().includes(searchTerm)
                )
                .map(gunung => `
                    <div class="gunung-card">
                        <div class="gunung-name">🏔️ ${gunung.nama}</div>
                        <div class="gunung-height">${gunung.ketinggian}</div>
                        <ul class="detail-list">
                            <li><span class="detail-label">📍 Lokasi:</span> ${gunung.lokasi}</li>
                            <li><span class="detail-label">🌋 Tipe:</span> ${gunung.tipe}</li>
                            <li><span class="detail-label">📝 Deskripsi:</span> ${gunung.deskripsi}</li>
                        </ul>
                        <div class="status ${gunung.status.toLowerCase()}">
                            ${gunung.status}
                        </div>
                    </div>
                `).join('');
        }

        // Event listener untuk search
        document.getElementById('searchInput').addEventListener('input', renderGunung);

        // Render awal
        renderGunung();
    </script>
</body>
</html>
