<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Presos Políticos De Cuba: Los Hermanos Perdomo</title>
    
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- Chart.js -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

    <!-- Fuentes -->
    <link href="https://fonts.googleapis.com/css2?family=Merriweather:ital,wght@0,300;0,400;0,700;1,300&family=Open+Sans:wght@400;600;700&display=swap" rel="stylesheet">

    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        'paper': '#F9F7F1',
                        'ink': '#2D3748',
                        'accent-red': '#9B2C2C',
                        'accent-blue': '#2C5282',
                        'highlight': '#E2E8F0',
                        'gold': '#D69E2E',
                    },
                    fontFamily: {
                        serif: ['Merriweather', 'serif'],
                        sans: ['Open Sans', 'sans-serif'],
                    }
                }
            }
        }
    </script>

    <style>
        body { background-color: #F9F7F1; color: #2D3748; }
        .timeline-line { position: absolute; left: 50%; transform: translateX(-50%); width: 4px; height: 100%; background-color: #CBD5E0; z-index: 0; }
        .chart-container { position: relative; width: 100%; max-width: 600px; height: 350px; max-height: 400px; margin: 0 auto; }
        @media (max-width: 768px) { .timeline-line { left: 20px; } .chart-container { height: 300px; } }
        .fade-in { animation: fadeIn 1s ease-in-out; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

        /* Efecto hover para tarjetas */
        .card-hover {
            transition: transform 0.2s ease, box-shadow 0.2s ease;
        }
        .card-hover:hover {
            transform: translateY(-4px);
            box-shadow: 0 10px 20px rgba(0,0,0,0.08);
        }
    </style>

</head>
<body class="font-sans antialiased selection:bg-accent-red selection:text-white">

    <!-- Navegación -->
    <nav class="sticky top-0 z-50 bg-paper/95 backdrop-blur border-b border-gray-200 shadow-sm">
        <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between h-16 items-center">
                <div class="flex-shrink-0 flex items-center">
                    <span class="font-serif font-bold text-xl tracking-tight text-accent-red">Presos Políticos<span class="text-ink"> De Cuba</span></span>
                </div>
                <div class="hidden md:flex space-x-8">
                    <button onclick="scrollToSection('profiles')" class="text-gray-600 hover:text-accent-red transition px-3 py-2 text-sm font-medium">Perfiles</button>
                    <button onclick="scrollToSection('timeline')" class="text-gray-600 hover:text-accent-red transition px-3 py-2 text-sm font-medium">Cronología</button>
                    <button onclick="scrollToSection('data')" class="text-gray-600 hover:text-accent-red transition px-3 py-2 text-sm font-medium">La Condena</button>
                    <button onclick="scrollToSection('voices')" class="text-gray-600 hover:text-accent-red transition px-3 py-2 text-sm font-medium">Testimonios</button>
                </div>
                <div class="md:hidden flex items-center">
                    <button id="mobile-menu-btn" class="text-gray-600 text-2xl">≡</button>
                </div>
            </div>
        </div>
        <div id="mobile-menu" class="hidden md:hidden bg-paper border-b border-gray-200">
            <div class="px-2 pt-2 pb-3 space-y-1">
                <button onclick="scrollToSection('profiles')" class="block w-full text-left px-3 py-2 text-base font-medium">Perfiles</button>
                <button onclick="scrollToSection('timeline')" class="block w-full text-left px-3 py-2 text-base font-medium">Cronología</button>
                <button onclick="scrollToSection('data')" class="block w-full text-left px-3 py-2 text-base font-medium">La Condena</button>
                <button onclick="scrollToSection('voices')" class="block w-full text-left px-3 py-2 text-base font-medium">Testimonios</button>
            </div>
        </div>
    </nav>

    <main class="max-w-5xl mx-auto px-4 sm:px-6 lg:px-8 py-10 space-y-20">

        <!-- Portada -->
        <section class="text-center space-y-6 fade-in">
            <div class="inline-block p-2 px-4 bg-accent-red text-white text-xs font-bold tracking-widest uppercase rounded-full">Campaña de Visibilización</div>
            <h1 class="text-4xl md:text-6xl font-serif font-bold text-ink leading-tight">
                Los Hermanos <span class="text-accent-blue">Perdomo</span>
            </h1>
            <p class="mt-4 max-w-2xl mx-auto text-xl text-gray-600 font-serif italic">
                Jorge y Nadir: El rostro de la injusticia contra quienes sueñan con una Cuba libre.
            </p>
            <div class="w-24 h-1 bg-accent-red mx-auto rounded"></div>
        </section>

        <!-- Introducción -->
        <section class="prose prose-lg mx-auto text-gray-600 text-justify">
            <p>
                Como parte del proyecto <strong>Presos Políticos De Cuba</strong>, presentamos la historia de <strong>Jorge y Nadir Martín Perdomo</strong>. 
                En San José de las Lajas, su único "delito" fue caminar pacíficamente pidiendo libertad el 11 de julio de 2021. 
                Hoy, sus condenas representan uno de los ejemplos más claros de la represión sistémica en la isla.
            </p>
        </section>

        <!-- Botones de compartir -->
        <section class="text-center space-y-4">
            <h2 class="text-2xl font-serif font-bold text-ink">Comparte esta campaña</h2>
            <p class="text-gray-600 max-w-2xl mx-auto text-sm">
                Ayuda a visibilizar el caso de los hermanos Perdomo y de todos los presos políticos en Cuba. Comparte esta página en tus redes.
            </p>
            <div class="flex flex-wrap gap-3 justify-center">
                <button
                    onclick="shareOnTwitter()"
                    class="px-4 py-2 bg-[#1DA1F2] text-white rounded-full text-sm font-semibold hover:bg-[#1A91DA] transition"
                >
                    Compartir en X (Twitter)
                </button>
                <button
                    onclick="shareOnFacebook()"
                    class="px-4 py-2 bg-[#1877F2] text-white rounded-full text-sm font-semibold hover:bg-[#145DBF] transition"
                >
                    Compartir en Facebook
                </button>
                <button
                    onclick="shareOnWhatsApp()"
                    class="px-4 py-2 bg-[#25D366] text-white rounded-full text-sm font-semibold hover:bg-[#1EBE5C] transition"
                >
                    Compartir en WhatsApp
                </button>
            </div>
        </section>

        <!-- Perfiles -->
        <section id="profiles" class="space-y-8 scroll-mt-24">
            <h2 class="text-3xl font-serif font-bold text-ink border-l-4 border-accent-blue pl-4">Los Protagonistas</h2>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
                <div class="bg-white p-6 rounded-lg shadow-md border-t-4 border-accent-blue card-hover">
                    <div class="flex items-center space-x-4 mb-4">
                        <div class="h-16 w-16 bg-gray-200 rounded-full flex items-center justify-center text-2xl">👨🏻‍🏫</div>
                        <div>
                            <h3 class="text-xl font-bold text-ink">Jorge Martín Perdomo</h3>
                            <span class="text-sm text-accent-red font-semibold">Sentencia: 8 Años</span>
                        </div>
                    </div>
                    <p class="text-sm text-gray-600">Informático y padre de familia. Su entereza en prisión ha sido denunciada por su madre como motivo de represalias adicionales.</p>
                </div>
                <div class="bg-white p-6 rounded-lg shadow-md border-t-4 border-accent-blue card-hover">
                    <div class="flex items-center space-x-4 mb-4">
                        <div class="h-16 w-16 bg-gray-200 rounded-full flex items-center justify-center text-2xl">👨🏻‍🏫</div>
                        <div>
                            <h3 class="text-xl font-bold text-ink">Nadir Martín Perdomo</h3>
                            <span class="text-sm text-accent-red font-semibold">Sentencia: 6 Años</span>
                        </div>
                    </div>
                    <p class="text-sm text-gray-600">Profesor de inglés. Su salud se ha visto afectada por las condiciones inhumanas de internamiento en Quivicán.</p>
                </div>
            </div>
        </section>

        <!-- Línea de tiempo -->
        <section id="timeline" class="space-y-8 scroll-mt-24">
            <h2 class="text-3xl font-serif font-bold text-ink border-l-4 border-accent-blue pl-4">Línea de Tiempo</h2>
            <div class="relative py-8">
                <div class="timeline-line"></div>
                <div id="timeline-container" class="space-y-12"></div>
            </div>
        </section>

        <!-- Datos / Gráficos -->
        <section id="data" class="space-y-10 scroll-mt-24 bg-white p-8 rounded-xl shadow-sm">
            <h2 class="text-3xl font-serif font-bold text-ink border-l-4 border-accent-red pl-4">Datos de la Injusticia</h2>
            <div class="grid grid-cols-1 lg:grid-cols-2 gap-10">
                <div class="chart-container"><canvas id="sentenceChart"></canvas></div>
                <div class="space-y-6">
                    <div class="bg-paper p-6 rounded-lg border-l-4 border-gold">
                        <h4 class="font-bold mb-2">Criminalización del Disenso</h4>
                        <p class="text-sm text-gray-600">En <strong>Presos Políticos De Cuba</strong>, documentamos cómo cargos como "Desacato" se usan para silenciar voces críticas.</p>
                    </div>
                    <div class="chart-container" style="height: 250px;"><canvas id="chargesContextChart"></canvas></div>
                </div>
            </div>
        </section>

        <!-- (Opcional) Sección de testimonios vacía por ahora -->
        <section id="voices" class="space-y-6 scroll-mt-24">
            <h2 class="text-3xl font-serif font-bold text-ink border-l-4 border-accent-blue pl-4">Testimonios</h2>
            <p class="text-sm text-gray-600">
                Próximamente añadiremos testimonios de familiares, activistas y organizaciones que acompañan el caso de los hermanos Perdomo.
            </p>
        </section>

        <!-- Footer -->
        <footer class="border-t border-gray-300 pt-10 pb-6 text-center">
            <p class="font-bold text-accent-red text-lg mb-2">Presos Políticos De Cuba</p>
            <p class="text-gray-500 text-sm italic">"Porque un pueblo que olvida a sus presos, olvida su libertad."</p>
        </footer>
    </main>

    <script>
        // Datos para la línea de tiempo
        const timelineEvents = [
            { date: "11J, 2021", title: "La Protesta", desc: "Marchan pacíficamente en San José de las Lajas.", icon: "📢", side: "left" },
            { date: "17 de Julio, 2021", title: "Arresto", desc: "Detenidos tras ser citados por la policía.", icon: "👮‍♂️", side: "right" },
            { date: "Enero, 2022", title: "Juicio Político", desc: "Sentenciados sin pruebas de violencia real.", icon: "⚖️", side: "left" },
            { date: "Hoy", title: "Resistencia", desc: "Permanecen en prisión bajo condiciones críticas.", icon: "✊", side: "right" }
        ];

        function renderTimeline() {
            const container = document.getElementById('timeline-container');
            container.innerHTML = timelineEvents.map(event => `
                <div class="relative flex justify-between items-center w-full md:w-3/4 mx-auto">
                    <div class="w-5/12 ${event.side === 'left' ? 'text-right' : 'order-last text-left'} px-4">
                        <div class="bg-white p-4 rounded shadow-sm border border-gray-100">
                            <h3 class="font-bold text-ink">${event.title}</h3>
                            <p class="text-accent-red text-xs font-bold">${event.date}</p>
                            <p class="text-xs text-gray-600">${event.desc}</p>
                        </div>
                    </div>
                    <div class="z-20 bg-paper shadow w-10 h-10 rounded-full flex items-center justify-center text-xl">${event.icon}</div>
                    <div class="w-5/12"></div>
                </div>
            `).join('');
        }

        // Gráficos con Chart.js
        function initCharts() {
            const ctx1 = document.getElementById('sentenceChart').getContext('2d');
            new Chart(ctx1, {
                type: 'bar',
                data: {
                    labels: ['Jorge (8 años)', 'Nadir (6 años)'],
                    datasets: [{ label: 'Años de Condena', data: [8, 6], backgroundColor: '#9B2C2C' }]
                },
                options: { responsive: true, maintainAspectRatio: false }
            });

            const ctx2 = document.getElementById('chargesContextChart').getContext('2d');
            new Chart(ctx2, {
                type: 'doughnut',
                data: {
                    labels: ['Desorden', 'Desacato', 'Atentado'],
                    datasets: [{ data: [50, 30, 20], backgroundColor: ['#2C5282', '#D69E2E', '#9B2C2C'] }]
                },
                options: { 
                    responsive: true, 
                    maintainAspectRatio: false, 
                    plugins: { 
                        title: { display: true, text: 'Cargos Típicos 11J' } 
                    } 
                }
            });
        }

        // Menú móvil
        document.getElementById('mobile-menu-btn').addEventListener('click', () => {
            document.getElementById('mobile-menu').classList.toggle('hidden');
        });

        // Scroll suave
        function scrollToSection(id) { 
            const el = document.getElementById(id);
            if (el) el.scrollIntoView({ behavior: 'smooth' }); 
        }

        // Texto y URL para compartir
        const shareUrl = 'https://tusitio.org/hermanos-perdomo'; // CAMBIA ESTO A TU URL REAL
        const shareText = 'Conoce la historia de los presos políticos Jorge y Nadir Martín Perdomo y súmate al reclamo de libertad para ellos y para Cuba. #PresosPoliticosDeCuba #11J';

        // Compartir en X/Twitter
        function shareOnTwitter() {
            const text = encodeURIComponent(shareText);
            const url = encodeURIComponent(shareUrl);
            const twitterUrl = `https://twitter.com/intent/tweet?text=${text}&url=${url}`;
            window.open(twitterUrl, '_blank');
        }

        // Compartir en Facebook
        function shareOnFacebook() {
            const url = encodeURIComponent(shareUrl);
            const text = encodeURIComponent(shareText);
            // Algunos navegadores aceptan también el parámetro "quote" para mostrar texto junto al enlace.[web:22][web:25][web:28]
            const facebookUrl = `https://www.facebook.com/sharer/sharer.php?u=${url}&quote=${text}`;
            window.open(facebookUrl, '_blank');
        }

        // Compartir en WhatsApp
        function shareOnWhatsApp() {
            const message = encodeURIComponent(`${shareText} ${shareUrl}`);
            // Formato recomendado para mensaje prellenado.[web:23][web:29]
            const whatsappUrl = `https://api.whatsapp.com/send?text=${message}`;
            window.open(whatsappUrl, '_blank');
        }

        // Inicialización
        window.onload = () => { 
            renderTimeline(); 
            initCharts(); 
        };
    </script>
</body>
</html>


Get Microsoft OneNote: https://aka.ms/GetOneNoteMobile
