<html lang="en">

<head>
    <title>PLEASE TERIMA GUE</title>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <!-- Tailwind CSS for styling -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Google Fonts: Inter -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style>
        /* Custom styles to apply the Inter font */
        body {
            font-family: 'Inter', sans-serif;
            position: relative; /* Needed for z-index stacking */
        }
        .raindrop {
            position: absolute;
            pointer-events: none;
            animation: fall linear;
            z-index: -1; /* Behind the content */
        }
        @keyframes fall {
            from {
                transform: translateY(-20vh) rotate(0deg);
            }
            to {
                transform: translateY(120vh) rotate(360deg);
            }
        }
    </style>
</head>

<body class="bg-gray-100 text-gray-800">
    <!-- Rain container -->
    <div id="rain-container" class="fixed inset-0 overflow-hidden pointer-events-none"></div>
    <!-- Main content container, added relative and z-index to stay on top of rain -->
    <div class="container mx-auto max-w-2xl p-4 sm:p-6 md:p-8 relative z-10">
        <header class="text-center mb-8">
            <img src="https://i.imgur.com/FWY7YJp.jpeg" alt="Profile Picture" class="w-24 h-24 rounded-full mx-auto mb-4 border-4 border-white shadow-lg">
            <!-- SAYA MEMPERBAIKI: "text-grey-900" menjadi "text-gray-900" (typo) -->
            <h1 class="text-3xl font-bold text-gray-900">Hai HAI HAII. TUHKAN BENERAN KAN BUKAN VIRUS. Uhm mungkin, gak guarantee 100% sih. #KitaHarusBerhati-hatiDalamBerinternet</h1>
            <p class="text-md text-gray-600 mt-1">Aku semangat bangetzszzzz untuk magang di HMDM. Please banget tonton video di bawah ini.</p>
        </header>
        <div class="mb-8 rounded-lg overflow-hidden shadow-2xl">
            <!-- IMPORTANT: Replace this with your actual YouTube video embed URL -->
            <iframe src="https://www.youtube.com/embed/dQw4w9WgXcQ" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen class="w-full h-80">
            </iframe>
        </div>
        <main>
            <h2 class="text-center text-xl font-semibold mb-6 text-gray-700">Professionally ini dokumen aku</h2>
            <div class="space-y-4">
                <a href="https://drive.google.com/file/d/1NG9AQ9JP1Wl6gaHTCk8vIVIiHC_t7DWG/view?usp=drive_link" target="_blank" class="block bg-white p-4 rounded-lg shadow-md hover:shadow-xl hover:bg-blue-50 transition-all duration-300 ease-in-out transform hover:-translate-y-1">
                    <div class="flex items-center">
                        <div class="flex-shrink-0">
                            <!-- Icon Placeholder -->
                            <svg class="w-6 h-6 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"></path>
                            </svg>
                        </div>
                        <div class="ml-4">
                            <p class="font-semibold text-lg">Curriculum Vitae (CV)</p>
                            <p class="text-sm text-gray-500">My pengalaman dan riwayat organisasi saya</p>
                        </div>
                    </div>
                </a>
                <a href="https://www.linkedin.com/in/arfaraddell/" target="_blank" class="block bg-white p-4 rounded-lg shadow-md hover:shadow-xl hover:bg-blue-50 transition-all duration-300 ease-in-out transform hover:-translate-y-1">
                    <div class="flex items-center">
                        <div class="flex-shrink-0">
                            <!-- Icon Placeholder -->
                            <svg class="w-6 h-6 text-blue-600" fill="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                                <path d="M19 0h-14c-2.761 0-5 2.239-5 5v14c0 2.761 2.239 5 5 5h14c2.762 0 5-2.239 5-5v-14c0-2.761-2.238-5-5-5zm-11 19h-3v-11h3v11zm-1.5-12.268c-.966 0-1.75-.79-1.75-1.764s.784-1.764 1.75-1.764 1.75.79 1.75 1.764-.783 1.764-1.75 1.764zm13.5 12.268h-3v-5.604c0-3.368-4-3.113-4 0v5.604h-3v-11h3v1.765c1.396-2.586 7-2.777 7 2.476v6.759z"></path>
                            </svg>
                        </div>
                        <div class="ml-4">
                            <p class="font-semibold text-lg">LinkedIn</p>
                            <p class="text-sm text-gray-500">My LinkedIn saya mine wow (Ini englishnya sarcastic ya)</p>
                        </div>
                    </div>
                </a>
            </div>
        </main>
        <!-- Footer -->
        <footer class="text-center mt-12">
            <p class="text-gray-500 text-sm">Dibuat dengan semangat oleh si si pasi Arfa Raddell</p>
        </footer>
    </div>
    <!-- Script untuk animasi hujan -->
    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const rainContainer = document.getElementById('rain-container');
            // --- GANTI GAMBAR DI SINI ---
            // Ganti URL di bawah ini dengan link ke gambar .png yang kamu mau.
            // Sebaiknya gunakan gambar .png yang kecil (misal: 30x30 pixel)
            // Saya pakai placeholder bintang biru untuk contoh:
            const rainImageUrl = 'https://i.imgur.com/jX7dtdP.png';
            function createRaindrop() {
                const drop = document.createElement('img');
                drop.src = rainImageUrl;
                drop.className = 'raindrop';
                // Randomize properties
                const size = Math.random() * 20 + 10; // Ukuran: 10px - 30px
                drop.style.width = size + 'px';
                drop.style.height = size + 'px';
                drop.style.left = Math.random() * 100 + 'vw'; // Posisi horizontal
                drop.style.opacity = Math.random() * 0.5 + 0.3; // Transparansi: 0.3 - 0.8
                const duration = Math.random() * 4 + 3; // Durasi jatuh: 3s - 7s
                drop.style.animationDuration = duration + 's';
                drop.style.animationDelay = Math.random() * 5 + 's'; // Mulai jatuh (delay
                rainContainer.appendChild(drop);
                // Hapus gambar setelah selesai jatuh
                setTimeout(() => {
                    drop.remove();
                }, (duration + 5) * 1000); // Hapus setelah (durasi + max delay)
            }
            // Buat gambar baru setiap 200ms
            // Ganti 200 untuk menambah/mengurangi kepadatan hujan
            setInterval(createRaindrop, 200); 
        });
    </script>

</body>
</html>

