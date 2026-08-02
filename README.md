# වාහන වෙළඳ දැන්වීම් වෙබ් අඩවිය (Vehicle Advertisement Website)

මෙම ලේඛනය තුළ ඔබගේ වාහන විකිණීමට දැන්වීම් (Ads) පළ කළ හැකි, නවීන සහ ආකර්ෂණීය **Single-Page Vehicle Sales Website** එකක සම්පූර්ණ කේතය (Source Code) සහ භාවිතය පිළිබඳ මාර්ගෝපදේශය අඩංගු වේ.

## 🛠️ මෙය භාවිතා කරන ආකාරය (How to Use):
1. පහත දක්වා ඇති HTML කේතය සම්පූර්ණයෙන්ම කොපි (Copy) කරගන්න.
2. ඔබේ පරිගණකයේ Notepad හෝ ඕනෑම Text Editor එකක් (VS Code වැනි) විවෘත කරන්න.
3. කේතය එහි අලවා (Paste), නම **`index.html`** ලෙස සේ이브 කරගන්න (Save as type: All Files දමා).
4. එම ගොනුව (File) මත Double Click කර ඕනෑම Web Browser එකක (Chrome, Edge, Firefox) විවෘත කර භාවිතා කළ හැක!

---

## 💻 වෙබ් අඩවියේ සම්පූර්ණ කේතය (Complete HTML/CSS/JS Code)

```html
<!DOCTYPE html>
<html lang="si">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AutoLanka - වාහන වෙළඳ දැන්වීම්</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Iskoola+Pota&family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Poppins', 'Iskoola Pota', sans-serif;
            background-color: #f3f4f6;
        }
    </style>
</head>
<body class="bg-gray-50 text-gray-800">

    <!-- Navbar -->
    <nav class="bg-blue-900 text-white shadow-lg sticky top-0 z-50">
        <div class="max-w-7xl mx-auto px-4 py-4 flex justify-between items-center">
            <div class="flex items-center space-x-2">
                <span class="text-2xl font-bold tracking-wider">🚗 AutoLanka<span class="text-yellow-400">.lk</span></span>
            </div>
            <div>
                <button onclick="openModal()" class="bg-yellow-500 hover:bg-yellow-600 text-blue-950 font-bold px-5 py-2 rounded-lg shadow transition duration-200">
                    + නව දැන්වීමක් දමන්න
                </button>
            </div>
        </div>
    </nav>

    <!-- Hero Section -->
    <header class="bg-gradient-to-r from-blue-900 to-indigo-800 text-white py-16 px-4 text-center">
        <div class="max-w-3xl mx-auto">
            <h1 class="text-4xl md:text-5xl font-extrabold mb-4">ශ්‍රී ලංකාවේ විශ්වාසනීයම වාහන වෙළඳපොළ</h1>
            <p class="text-lg text-blue-200 mb-8">ඔබට අවශ්‍ය මෝටර් රථ, වැන්, ජීප් රථ සහ බයිසිකල් පහසුවෙන් සොයාගන්න හෝ ඔබේ වාහනය අදම විකුණන්න.</p>
            
            <!-- Search Bar -->
            <div class="bg-white p-3 rounded-xl shadow-lg flex flex-col md:flex-row gap-3">
                <input type="text" id="searchInput" placeholder="වාහන නම හෝ ස්ථානය සොයන්න..." class="flex-grow px-4 py-3 rounded-lg border border-gray-300 focus:outline-none focus:border-blue-500 text-gray-800">
                <select id="categoryFilter" class="px-4 py-3 rounded-lg border border-gray-300 focus:outline-none focus:border-blue-500 text-gray-800">
                    <option value="">සියලුම කාණ්ඩ (All)</option>
                    <option value="Car">මෝටර් රථ (Cars)</option>
                    <option value="SUV">ජීප් / SUV (SUVs)</option>
                    <option value="Van">වැන් රථ (Vans)</option>
                    <option value="Bike">මෝටර් බයිසිකල් (Bikes)</option>
                </select>
                <button onclick="filterAds()" class="bg-blue-900 hover:bg-blue-800 text-white font-semibold px-6 py-3 rounded-lg transition duration-200">
                    සොයන්න
                </button>
            </div>
        </div>
    </header>

    <!-- Main Content: Listings -->
    <main class="max-w-7xl mx-auto px-4 py-12">
        <div class="flex justify-between items-center mb-8">
            <h2 class="text-2xl font-bold text-gray-900 border-l-4 border-blue-900 pl-3">මෑතකදී එකතු කළ දැන්වීම්</h2>
            <span id="adCount" class="text-sm text-gray-500 font-medium">දැන්වීම් 0 ක් ඇත</span>
        </div>

        <!-- Ads Grid -->
        <div id="adsContainer" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
            <!-- Dynamic Ads will load here -->
        </div>
    </main>

    <!-- Post Ad Modal -->
    <div id="adModal" class="fixed inset-0 bg-black bg-opacity-50 hidden justify-center items-center z-50 p-4">
        <div class="bg-white rounded-2xl max-w-lg w-full p-6 shadow-2xl relative max-h-[90vh] overflow-y-auto">
            <button onclick="closeModal()" class="absolute top-4 right-4 text-gray-400 hover:text-gray-600 text-2xl font-bold">&times;</button>
            <h3 class="text-2xl font-bold text-blue-900 mb-6">වාහන දැන්වීමක් ඇතුළත් කරන්න</h3>
            
            <form id="adForm" onsubmit="saveAd(event)" class="space-y-4">
                <div>
                    <label class="block text-sm font-semibold text-gray-700 mb-1">වාහනයේ නම / මාදිලිය (Title)</label>
                    <input type="text" id="carTitle" required placeholder="උදා: Toyota Premio F-Package 2016" class="w-full px-4 py-2 border rounded-lg focus:ring-2 focus:ring-blue-500 focus:outline-none">
                </div>
                
                <div class="grid grid-cols-2 gap-4">
                    <div>
                        <label class="block text-sm font-semibold text-gray-700 mb-1">කාණ්ඩය (Category)</label>
                        <select id="carCategory" class="w-full px-4 py-2 border rounded-lg focus:ring-2 focus:ring-blue-500 focus:outline-none">
                            <option value="Car">මෝටර් රථ (Car)</option>
                            <option value="SUV">ජීප් / SUV</option>
                            <option value="Van">වැන් රථ (Van)</option>
                            <option value="Bike">මෝටර් බයිසිකල් (Bike)</option>
                        </select>
                    </div>
                    <div>
                        <label class="block text-sm font-semibold text-gray-700 mb-1">මිළ (LKR)</label>
                        <input type="number" id="carPrice" required placeholder="උදා: 12500000" class="w-full px-4 py-2 border rounded-lg focus:ring-2 focus:ring-blue-500 focus:outline-none">
                    </div>
                </div>

                <div class="grid grid-cols-2 gap-4">
                    <div>
                        <label class="block text-sm font-semibold text-gray-700 mb-1">නිෂ්පාදිත වර්ෂය (Year)</label>
                        <input type="number" id="carYear" required placeholder="උදා: 2016" class="w-full px-4 py-2 border rounded-lg focus:ring-2 focus:ring-blue-500 focus:outline-none">
                    </div>
                    <div>
                        <label class="block text-sm font-semibold text-gray-700 mb-1">ධාවනය කළ දුර (Mileage)</label>
                        <input type="text" id="carMileage" required placeholder="උදා: 45,000 km" class="w-full px-4 py-2 border rounded-lg focus:ring-2 focus:ring-blue-500 focus:outline-none">
                    </div>
                </div>

                <div>
                    <label class="block text-sm font-semibold text-gray-700 mb-1">ස්ථානය (Location)</label>
                    <input type="text" id="carLocation" required placeholder="උදා: කොළඹ" class="w-full px-4 py-2 border rounded-lg focus:ring-2 focus:ring-blue-500 focus:outline-none">
                </div>

                <div>
                    <label class="block text-sm font-semibold text-gray-700 mb-1">ඡායාරූප සබැඳිය (Image URL)</label>
                    <input type="url" id="carImage" required placeholder="රූපයක Direct Link එකක් දෙන්න (උදා: Unsplash)" class="w-full px-4 py-2 border rounded-lg focus:ring-2 focus:ring-blue-500 focus:outline-none">
                </div>

                <div>
                    <label class="block text-sm font-semibold text-gray-700 mb-1">දුරකථන අංකය (Contact Number)</label>
                    <input type="tel" id="carContact" required placeholder="උදා: 0771234567" class="w-full px-4 py-2 border rounded-lg focus:ring-2 focus:ring-blue-500 focus:outline-none">
                </div>

                <button type="submit" class="w-full bg-blue-900 hover:bg-blue-800 text-white font-bold py-3 rounded-lg shadow transition duration-200 mt-4">
                    දැන්වීම පළ කරන්න
                </button>
            </form>
        </div>
    </div>

    <!-- Footer -->
    <footer class="bg-blue-950 text-white py-8 mt-16 text-center">
        <p>&copy; 2026 AutoLanka.lk - සියලු හිමිකම් ඇවිරිණි.</p>
    </footer>

    <!-- JavaScript Logic -->
    <script>
        let ads = JSON.parse(localStorage.getItem('vehicleAds')) || [
            {
                id: 1,
                title: 'Toyota Premio F-Package',
                category: 'Car',
                price: '11800000',
                year: '2015',
                mileage: '62,000 km',
                location: 'කොළඹ',
                image: 'https://images.unsplash.com/photo-1550355291-bbee04a92027?auto=format&fit=crop&w=600&q=80',
                contact: '0771234567'
            },
            {
                id: 2,
                title: 'Honda Vezel Z Grade',
                category: 'SUV',
                price: '10500000',
                year: '2016',
                mileage: '54,000 km',
                location: 'ගම්පහ',
                image: 'https://images.unsplash.com/photo-1533473359331-0135ef1b58bf?auto=format&fit=crop&w=600&q=80',
                contact: '0719876543'
            }
        ];

        function renderAds(adsToRender = ads) {
            const container = document.getElementById('adsContainer');
            const countEl = document.getElementById('adCount');
            container.innerHTML = '';
            countEl.innerText = `දැන්වීම් ${adsToRender.length} ක් ඇත`;

            if(adsToRender.length === 0) {
                container.innerHTML = `<p class="col-span-full text-center text-gray-500 py-12">දැන්වීම් කිසිවක් හමු නොවීය.</p>`;
                return;
            }

            adsToRender.forEach(ad => {
                container.innerHTML += `
                    <div class="bg-white rounded-2xl shadow-md overflow-hidden hover:shadow-xl transition duration-300 flex flex-col justify-between border border-gray-100">
                        <div>
                            <div class="relative h-48 overflow-hidden">
                                <img src="${ad.image}" alt="${ad.title}" class="w-full h-full object-cover hover:scale-105 transition duration-300">
                                <span class="absolute top-3 left-3 bg-blue-900 text-white text-xs font-bold px-3 py-1 rounded-full shadow">${ad.category}</span>
                            </div>
                            <div class="p-5">
                                <h3 class="text-xl font-bold text-gray-900 mb-1">${ad.title}</h3>
                                <p class="text-2xl font-extrabold text-blue-900 mb-4">රු. ${Number(ad.price).toLocaleString()} <span class="text-xs text-gray-500 font-normal">සාකච්ඡා කළ හැක</span></p>
                                
                                <div class="grid grid-cols-2 gap-2 text-sm text-gray-600 bg-gray-50 p-3 rounded-xl mb-4">
                                    <div>📅 වර්ෂය: <span class="font-semibold text-gray-800">${ad.year}</span></div>
                                    <div>🛣️ ධාවනය: <span class="font-semibold text-gray-800">${ad.mileage}</span></div>
                                    <div>📍 ස්ථානය: <span class="font-semibold text-gray-800">${ad.location}</span></div>
                                </div>
                            </div>
                        </div>
                        <div class="px-5 pb-5">
                            <a href="tel:${ad.contact}" class="block text-center bg-green-600 hover:bg-green-700 text-white font-bold py-2.5 rounded-xl transition duration-200 shadow">
                                📞 අමතන්න: ${ad.contact}
                            </a>
                        </div>
                    </div>
                `;
            });
        }

        function openModal() {
            document.getElementById('adModal').classList.remove('hidden');
            document.getElementById('adModal').classList.add('flex');
        }

        function closeModal() {
            document.getElementById('adModal').classList.add('hidden');
            document.getElementById('adModal').classList.remove('flex');
        }

        function saveAd(e) {
            e.preventDefault();
            const newAd = {
                id: Date.now(),
                title: document.getElementById('carTitle').value,
                category: document.getElementById('carCategory').value,
                price: document.getElementById('carPrice').value,
                year: document.getElementById('carYear').value,
                mileage: document.getElementById('carMileage').value,
                location: document.getElementById('carLocation').value,
                image: document.getElementById('carImage').value,
                contact: document.getElementById('carContact').value
            };

            ads.unshift(newAd);
            localStorage.setItem('vehicleAds', JSON.stringify(ads));
            renderAds();
            closeModal();
            document.getElementById('adForm').reset();
            alert('ඔබගේ දැන්වීම සාර්ථකව එකතු කරන ලදී!');
        }

        function filterAds() {
            const query = document.getElementById('searchInput').value.toLowerCase();
            const category = document.getElementById('categoryFilter පහසුකම්').value || document.getElementById('categoryFilter').value;

            const filtered = ads.filter(ad => {
                const matchesQuery = ad.title.toLowerCase().includes(query) || ad.location.toLowerCase().includes(query);
                const matchesCategory = category === "" || ad.category === category;
                return matchesQuery && matchesCategory;
            });

            renderAds(filtered);
        }

        renderAds();
    </script>
</body>
</html>
```

## ✨ විශේෂාංග (Features):
1. **නවීන පෙනුම (Modern UI):** Tailwind CSS සමඟින් නිර්මාණය කර ඇති බැවින් Mobile සහ Desktop දෙකෙහිම ඉතා අලංකාර ලෙස පෙනේ.
2. **දැන්වීම් එකතු කිරීම (Post Ads):** ඕනෑම කෙනෙකුට තමන්ගේ වාහනයේ විස්තර, මිල සහ පින්තූර ඇතුළත් කර ක්ෂණිකව වෙබ් අඩවියට දැන්වීමක් දැමිය හැක.
3. **Local Storage:** ඔබ දමන දැන්වීම් ඔබගේ බ්‍රව්සරයේ සුරැකෙන නිසා නැවත පිටුව Refresh කළත් මැකී යන්නේ නැත.
4. **සෙවීම සහ පෙරීම (Search & Filter):** වාහන වර්ගය සහ නම අනුව අවශ්‍ය වාහනය පහසුවෙන් සොයාගත හැක.
