<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gala El Jireh - Club Juvenil</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@400;700;900&family=Montserrat:wght@300;400;600;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --gold: #d4af37;
            --gold-dark: #aa8a2e;
            --dark-bg: #05070a;
        }
        body {
            background-color: var(--dark-bg);
            color: #e2e8f0;
            font-family: 'Montserrat', sans-serif;
            background-image: 
                radial-gradient(circle at top, rgba(212, 175, 55, 0.15) 0%, transparent 70%),
                linear-gradient(to bottom, #05070a, #0a0e14);
            background-attachment: fixed;
        }
        .font-cinzel { font-family: 'Cinzel', serif; }
        .gold-text { color: var(--gold); }
        
        .glass-card {
            background: rgba(15, 18, 24, 0.85);
            backdrop-filter: blur(16px);
            border: 1px solid rgba(212, 175, 55, 0.2);
            border-radius: 28px;
        }

        .nominee-card {
            transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            background: rgba(255, 255, 255, 0.02);
        }

        .photo-frame {
            width: 140px;
            height: 140px;
            border-radius: 50%;
            border: 2px solid var(--gold);
            padding: 5px;
            margin: 0 auto 1.5rem;
            overflow: hidden;
            background: #000;
        }
        .photo-frame img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            border-radius: 50%;
        }

        .cat-tab {
            padding: 12px 24px;
            border-radius: 16px;
            font-size: 10px;
            text-transform: uppercase;
            font-weight: 700;
            letter-spacing: 0.15em;
            transition: all 0.3s;
            border: 1px solid rgba(212, 175, 55, 0.1);
            color: #94a3b8;
            white-space: nowrap;
        }
        .cat-tab.active {
            background: linear-gradient(135deg, var(--gold), #f3e5ab);
            color: black;
            box-shadow: 0 8px 20px rgba(212, 175, 55, 0.4);
        }

        .btn-gold {
            background: linear-gradient(135deg, #b8860b 0%, #d4af37 100%);
            color: black;
            font-weight: 800;
            text-transform: uppercase;
            letter-spacing: 0.15em;
            transition: all 0.3s;
        }

        .phase-indicator {
            padding: 4px 14px;
            border-radius: 100px;
            font-size: 9px;
            font-weight: 900;
            text-transform: uppercase;
            letter-spacing: 2px;
        }

        .input-elegant {
            background: rgba(0,0,0,0.6);
            border: 1px solid rgba(255,255,255,0.1);
            border-radius: 1rem;
            padding: 1.25rem;
            color: white;
            width: 100%;
            outline: none;
            transition: border-color 0.3s;
        }
        .input-elegant:focus {
            border-color: var(--gold);
        }

        @keyframes fadeInUp {
            from { opacity: 0; transform: translateY(30px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .animate-up { animation: fadeInUp 0.6s ease-out forwards; }
        .no-scrollbar::-webkit-scrollbar { display: none; }
    </style>
</head>
<body class="min-h-screen pb-20">

    <!-- Encabezado Principal -->
    <header class="pt-16 pb-12 text-center px-4">
        <div class="mb-4">
            <h2 class="font-cinzel gold-text tracking-[0.4em] text-sm md:text-base font-bold uppercase">Club Juvenil El Jireh</h2></div>
        <div class="inline-block border-y border-gold/30 py-2 px-8 mb-6">
            <p class="font-cinzel text-gray-400 tracking-[0.6em] text-[10px] font-bold uppercase">Dios Proveerá</p>
        </div>
        <h1 class="text-5xl md:text-8xl font-cinzel font-black gold-text tracking-tighter mb-6">CENA DE GALA</h1>
        
        <div id="statusBadgeContainer" class="flex justify-center gap-2 mt-4"></div>
    </header>

    <main class="max-w-6xl mx-auto px-6">
        
        <!-- SECCIÓN REGISTRO (NOMINACIONES) -->
        <section id="nominationSection" class="glass-card p-8 md:p-14 mb-20 relative overflow-hidden hidden">
            <h2 class="text-2xl font-cinzel gold-text mb-10 tracking-widest uppercase flex items-center border-b border-gold/10 pb-4">
                <span class="mr-4 text-3xl">📜</span> Registro de Nominados
            </h2>
            
            <div class="grid grid-cols-1 lg:grid-cols-3 gap-12">
                <div class="text-center">
                    <div id="photoPreview" class="photo-frame flex items-center justify-center bg-white/5 border-dashed border-gold/40">
                        <span class="text-gray-500 text-[10px] uppercase font-bold tracking-widest">Subir Foto</span>
                    </div>
                    <div class="relative overflow-hidden mt-4 max-w-[200px] mx-auto">
                        <button class="w-full py-4 rounded-2xl border border-gold/20 text-[10px] uppercase font-bold gold-text">Elegir Imagen</button>
                        <input type="file" id="inputPhoto" accept="image/*" onchange="previewImage(this)" class="absolute inset-0 opacity-0 cursor-pointer">
                    </div>
                </div>

                <div class="lg:col-span-2 space-y-8">
                    <div class="space-y-6">
                        <div>
                            <label class="block text-[10px] uppercase text-gold/70 font-bold mb-3 tracking-widest">Seleccionar Categoría</label>
                            <select id="inputCat" onchange="toggleFormMode()" class="input-elegant appearance-none">
                                <option value="pareja">La Pareja más Bonita</option>
                                <option value="traje">El Mejor Traje de Gala</option>
                                <option value="vestido">El Mejor Vestido de Gala</option>
                                <option value="chispa">Mejor Actitud / Chispa</option>
                            </select>
                        </div>

                        <!-- Campos para Nominaciones Individuales -->
                        <div id="individualFields" class="hidden">
                            <label class="block text-[10px] uppercase text-gold/70 font-bold mb-3 tracking-widest">Nombre y Apellido Completo (Obligatorio)</label>
                            <input type="text" id="inputNameSingle" placeholder="Ej: Carlos Rodríguez" class="input-elegant">
                        </div>

                        <!-- Campos para Nominación de Parejas -->
<div id="coupleFields" class="grid grid-cols-1 md:grid-cols-2 gap-6">
                            <div>
                                <label class="block text-[10px] uppercase text-gold/70 font-bold mb-3 tracking-widest">Nombre y Apellido del Caballero</label>
                                <input type="text" id="inputNameMale" placeholder="Nombre completo" class="input-elegant">
                            </div>
                            <div>
                                <label class="block text-[10px] uppercase text-gold/70 font-bold mb-3 tracking-widest">Nombre y Apellido de la Dama</label>
                                <input type="text" id="inputNameFemale" placeholder="Nombre completo" class="input-elegant">
                            </div>
                        </div>
                    </div>
                    
                    <button onclick="handleNomination()" class="btn-gold w-full py-6 rounded-2xl text-xs shadow-2xl mt-4">Confirmar Inscripción</button>
                </div>
            </div>
        </section>

        <!-- SECCIÓN VOTACIONES -->
        <section id="votingSection" class="mb-20 hidden">
            <div class="flex flex-col items-center mb-16 text-center">
                <h2 class="font-cinzel gold-text text-3xl mb-4 tracking-[0.3em] uppercase font-black">Salón de Votos</h2>
                <div class="h-1 w-24 bg-gradient-to-r from-transparent via-gold to-transparent mb-10"></div>
                
                <div class="flex overflow-x-auto max-w-full gap-4 pb-6 no-scrollbar px-4">
                    <button onclick="setVoteCategory('pareja')" class="cat-tab active" id="btn-pareja">Pareja</button>
                    <button onclick="setVoteCategory('traje')" class="cat-tab" id="btn-traje">Traje</button>
                    <button onclick="setVoteCategory('vestido')" class="cat-tab" id="btn-vestido">Vestido</button>
                    <button onclick="setVoteCategory('chispa')" class="cat-tab" id="btn-chispa">Actitud</button>
                </div>
            </div>
            <div id="votingList" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-10"></div>
        </section>

        <!-- SECCIÓN SISTEMA CERRADO -->
        <section id="closedSection" class="glass-card p-20 text-center hidden">
            <div class="text-6xl mb-6">🔒</div>
            <h3 class="font-cinzel gold-text text-2xl tracking-widest mb-4">SISTEMA CERRADO</h3>
            <p class="text-gray-500 uppercase text-[10px] tracking-[0.4em]">Por favor, espere indicaciones del administrador.</p>
        </section>
    </main>

    <!-- Botón de Acceso Admin -->
    <div class="fixed bottom-6 right-6 z-40">
        <button onclick="showAdminLogin()" class="w-14 h-14 rounded-full glass-card border-gold/40 flex items-center justify-center shadow-2xl hover:scale-110 transition-transform bg-black/40">
            <span class="text-xl opacity-60">⚙️</span>
        </button>
    </div>   <!-- Modal Login Admin -->
    <div id="adminLoginModal" class="fixed inset-0 bg-black/95 hidden flex items-center justify-center z-50 backdrop-blur-xl">
        <div class="glass-card p-12 w-full max-w-sm text-center">
            <h3 class="font-cinzel gold-text text-lg mb-8 tracking-widest uppercase font-black">Admin Access</h3>
            <input type="password" id="adminPass" placeholder="••••" class="w-full bg-black/50 border border-white/10 rounded-2xl p-5 text-center mb-8 text-white tracking-[0.8em] text-xl">
            <div class="flex flex-col gap-4">
                <button onclick="checkAdminPass()" class="btn-gold py-5 rounded-2xl text-[11px]">Ingresar</button>
                <button onclick="closeModals()" class="text-[10px] text-gray-500 uppercase tracking-widest hover:text-white transition">Cerrar</button>
            </div>
        </div>
    </div>

    <!-- Panel Maestro de Control -->
    <div id="adminPanel" class="fixed inset-0 bg-[#05070a] z-[60] p-8 hidden overflow-y-auto">
        <div class="max-w-4xl mx-auto pb-32">
            <div class="flex justify-between items-center mb-12 border-b border-gold/20 pb-8">
                <h2 class="text-3xl font-cinzel gold-text tracking-widest uppercase font-black">Panel Maestro</h2>
                <button onclick="closeAdminPanel()" class="text-gray-500 text-4xl">&times;</button>
            </div>
            
            <div class="grid grid-cols-1 md:grid-cols-3 gap-6 mb-16">
                <button onclick="updatePhase('nominations')" id="phaseBtn-nominations" class="p-6 rounded-3xl border border-white/5 bg-white/5 text-center transition-all">
                    <div class="text-2xl mb-2">📝</div>
                    <div class="text-[10px] font-bold uppercase tracking-widest text-gray-400">Nominaciones</div>
                </button>
                <button onclick="updatePhase('voting')" id="phaseBtn-voting" class="p-6 rounded-3xl border border-white/5 bg-white/5 text-center transition-all">
                    <div class="text-2xl mb-2">🗳️</div>
                    <div class="text-[10px] font-bold uppercase tracking-widest text-gray-400">Votaciones</div>
                </button>
                <button onclick="updatePhase('closed')" id="phaseBtn-closed" class="p-6 rounded-3xl border border-white/5 bg-white/5 text-center transition-all">
                    <div class="text-2xl mb-2">⏸️</div>
                    <div class="text-[10px] font-bold uppercase tracking-widest text-gray-400">Cerrar Todo</div>
                </button>
            </div>

            <div id="adminStats" class="space-y-12"></div>
            
            <div class="mt-24 text-center">
                <button onclick="clearSystemData()" class="text-red-900 text-[10px] font-black uppercase tracking-widest px-8 py-4 border border-red-900/20 rounded-full hover:bg-red-950/20 transition">⚠️ Reiniciar Todo</button>
            </div>
        </div>
    </div>

    <!-- Toast de Notificación -->
    <div id="toast" class="fixed top-10 left-1/2 -translate-x-1/2 bg-white text-black px-12 py-5 rounded-full text-[11px] font-black shadow-2xl hidden z-[100] uppercase tracking-widest transition-all"></div>

    <script>
        // ESTADO GLOBAL
        const STATE = {
            nominees: JSON.parse(localStorage.getItem('jireh_v8_data')) || [],
            votes: JSON.parse(localStorage.getItem('jireh_v8_votes')) || {},
            phase: localStorage.getItem('jireh_v8_phase') || 'nominations'
        };

        const categories = {
            pareja: "La Pareja más Bonita",
            traje: "El Mejor Traje de Gala",
            vestido: "El Mejor Vestido de Gala",
            chispa: "Mejor Actitud / Chispa"
        };

        let currentCategory = 'pareja';
        let currentPhotoBase64 = null;

        function saveState() {
            localStorage.setItem('jireh_v8_data', JSON.stringify(STATE.nominees));
            localStorage.setItem('jireh_v8_votes', JSON.stringify(STATE.votes));
            localStorage.setItem('jireh_v8_phase', STATE.phase);
        }         // LÓGICA DE FORMULARIO DINÁMICO
        function toggleFormMode() {
            const cat = document.getElementById('inputCat').value;
            const ind = document.getElementById('individualFields');
            const cpl = document.getElementById('coupleFields');
            
            if(cat === 'pareja') {
                ind.classList.add('hidden');
                cpl.classList.remove('hidden');
            } else {
                ind.classList.remove('hidden');
                cpl.classList.add('hidden');
            }
        }

        // VALIDACIÓN DE NOMBRE Y APELLIDO
        function isValidFullName(str) {
            if(!str) return false;
            const words = str.trim().split(/\s+/);
            return words.length >= 2;
        }

        // MANEJO DE INSCRIPCIÓN
        function handleNomination() {
            const cat = document.getElementById('inputCat').value;
            let finalName = "";

            if(cat === 'pareja') {
                const male = document.getElementById('inputNameMale').value.trim();
                const female = document.getElementById('inputNameFemale').value.trim();
                
                if(!isValidFullName(male) || !isValidFullName(female)) {
                    return showToast("Debe ingresar Nombre y Apellido de AMBOS ⚠️", true);
                }
                finalName = `${male} y ${female}`;
            } else {
                const name = document.getElementById('inputNameSingle').value.trim();
                if(!isValidFullName(name)) {
                    return showToast("Debe ingresar Nombre y Apellido completo ⚠️", true);
                }
                finalName = name;
            }

            STATE.nominees.push({ 
                id: Date.now(), 
                name: finalName, 
                category: cat, 
                photo: currentPhotoBase64, 
                votes: 0 
            });
            
            saveState();
            
            // Limpieza de campos
            document.getElementById('inputNameSingle').value = "";
            document.getElementById('inputNameMale').value = "";
            document.getElementById('inputNameFemale').value = "";
            document.getElementById('inputPhoto').value = "";
            document.getElementById('photoPreview').innerHTML = `<span class="text-gray-500 text-[10px] uppercase font-bold tracking-widest">Subir Foto</span>`;
            currentPhotoBase64 = null;
            showToast("Nominación Exitosa ✨");
        }

        // ACTUALIZACIÓN DE INTERFAZ POR FASE
        function updatePhase(newPhase) {
            STATE.phase = newPhase;
            saveState();
            refreshUI();
            showToast(`SISTEMA: ${newPhase.toUpperCase()}`);
        }

        function refreshUI() {
            const container = document.getElementById('statusBadgeContainer');
            let badge = '';
            if(STATE.phase === 'nominations') badge = '<span class="phase-indicator bg-blue-900/30 text-blue-400 border border-blue-400/30">Inscripciones Abiertas</span>';
            if(STATE.phase === 'voting') badge = '<span class="phase-indicator bg-gold/20 text-gold border border-gold/30">Votaciones Activas</span>';
            if(STATE.phase === 'closed') badge = '<span class="phase-indicator bg-red-900/30 text-red-400 border border-red-400/30">Evento en Pausa</span>';
            container.innerHTML = badge;
          document.getElementById('nominationSection').classList.toggle('hidden', STATE.phase !== 'nominations');
            document.getElementById('votingSection').classList.toggle('hidden', STATE.phase !== 'voting');
            document.getElementById('closedSection').classList.toggle('hidden', STATE.phase !== 'closed');

            // Actualizar botones de fase en panel admin
            document.querySelectorAll('[id^="phaseBtn-"]').forEach(btn => {
                const p = btn.id.split('-')[1];
                btn.classList.toggle('border-gold', p === STATE.phase);
                btn.classList.toggle('bg-gold/10', p === STATE.phase);
            });

            if(STATE.phase === 'voting') renderVotes();
            if(!document.getElementById('adminPanel').classList.contains('hidden')) renderAdminStats();
            toggleFormMode();
        }

        // PREVIEW DE IMAGEN
        function previewImage(input) {
            if (input.files && input.files[0]) {
                const reader = new FileReader();
                reader.onload = e => {
                    currentPhotoBase64 = e.target.result;
                    document.getElementById('photoPreview').innerHTML = `<img src="${e.target.result}" class="animate-up">`;
                };
                reader.readAsDataURL(input.files[0]);
            }
        }
        
        // RENDERIZADO DE VOTACIÓN
        function setVoteCategory(cat) {
            currentCategory = cat;
            document.querySelectorAll('.cat-tab').forEach(b => b.classList.toggle('active', b.id === `btn-${cat}`));
            renderVotes();
        }

        function renderVotes() {
            const list = document.getElementById('votingList');
            list.innerHTML = "";
            const filtered = STATE.nominees.filter(n => n.category === currentCategory);
            
            if(filtered.length === 0) {
                list.innerHTML = `<div class="col-span-full py-20 text-center opacity-20 text-[10px] tracking-widest font-bold uppercase italic">Sin candidatos en esta sección</div>`;
                return;
            }

            filtered.forEach((n, idx) => {
                const votedId = STATE.votes[currentCategory];
                const isSelected = votedId === n.id;
                
                const card = document.createElement('div');
                card.className = `glass-card p-10 nominee-card flex flex-col items-center animate-up ${isSelected ? 'border-gold bg-gold/10' : ''}`;
                card.style.animationDelay = `${idx * 0.1}s`;
                
                card.innerHTML = `
                    <div class="photo-frame">${n.photo ? `<img src="${n.photo}">` : `<div class="h-full w-full flex items-center justify-center text-3xl font-bold gold-text">${n.name[0]}</div>`}</div>
                    <h3 class="text-base font-bold gold-text mb-2 text-center uppercase tracking-wide px-4">${n.name}</h3>
                    <p class="text-[9px] text-gray-600 uppercase tracking-widest mb-8 font-black">Candidato Oficial</p>
                    <button onclick="vote(${n.id})" ${votedId ? 'disabled' : ''} 
                            class="w-full py-4 rounded-2xl text-[10px] font-black uppercase tracking-widest transition-all
                            ${isSelected ? 'bg-white text-black shadow-xl scale-105' : (votedId ? 'opacity-30 border border-gray-900 cursor-not-allowed' : 'btn-gold hover:scale-105')}">
                        ${isSelected ? 'Confirmado' : (votedId ? 'Cerrado' : 'Emitir Voto')}
                    </button>
                `;
                list.appendChild(card);
            });
        }

        function vote(id) {
            if(STATE.votes[currentCategory]) return;
            const nominee = STATE.nominees.find(n => n.id === id);
            if(nominee) {
                nominee.votes++;
                STATE.votes[currentCategory] = id;
                saveState();
                renderVotes();
                showToast("Voto Registrado con Éxito 👑");
            }
        }

        // PANEL DE ESTADÍSTICAS ADMIN
        function renderAdminStats() {
            const stats = document.getElementById('adminStats');
            stats.innerHTML = "";

            Object.keys(categories).forEach(key => {
                const catNominees = STATE.nominees.filter(n => n.category === key).sort((a,b) => b.votes - a.votes);
                const totalVotes = catNominees.reduce((acc, n) => acc + n.votes, 0);

                let html = `
                    <div class="glass-card p-10 border-gold/10">
                        <div class="flex justify-between items-end mb-8 border-b border-white/5 pb-4">
                            <h3 class="gold-text font-cinzel text-lg tracking-widest uppercase font-black">${categories[key]}</h3>
                            <span class="text-[10px] text-gray-500 font-bold uppercase">${totalVotes} Votos en total</span>
                        </div>
                        <div class="space-y-8">
                `;

                catNominees.forEach(n => {
                    const percentage = totalVotes > 0 ? ((n.votes / totalVotes) * 100).toFixed(1) : 0;
                    html += `
                        <div class="flex items-center gap-6">
                            <div class="w-12 h-12 rounded-full border border-gold/30 overflow-hidden flex-shrink-0">
                                ${n.photo ? `<img src="${n.photo}" class="w-full h-full object-cover">` : `<div class="h-full w-full bg-white/5 flex items-center justify-center text-[10px] gold-text">${n.name[0]}</div>`}
                            </div>
                            <div class="flex-1">
                                <div class="flex justify-between items-end mb-2">
                                    <span class="text-[11px] font-bold uppercase truncate max-w-[200px]">${n.name}</span>
                                    <span class="text-xs gold-text font-black">${percentage}% <span class="text-[9px] opacity-40 ml-1">(${n.votes})</span></span>
                                </div>
                                <div class="w-full bg-black h-1.5 rounded-full overflow-hidden border border-white/5">
                                    <div class="bg-gradient-to-r from-gold-dark to-white h-full transition-all duration-1000" style="width: ${percentage}%"></div>
                                </div>
                            </div>
                        </div>
                    `;
                });
                
                if(catNominees.length === 0) html += `<p class="text-[10px] text-gray-700 italic text-center">No hay nominados aún</p>`;
                html += `</div></div>`;
                stats.innerHTML += html;
            });
        }

        // FUNCIONES ADMIN LOGIN
        function showAdminLogin() { document.getElementById('adminLoginModal').classList.remove('hidden'); }
        function closeModals() { document.getElementById('adminLoginModal').classList.add('hidden'); }
        function checkAdminPass() {
            if(document.getElementById('adminPass').value === '1234') {
                closeModals();
                document.getElementById('adminPass').value = "";
                document.getElementById('adminPanel').classList.remove('hidden');
                renderAdminStats();
            } else { showToast("Contraseña Incorrecta ❌", true); }
        }
        function closeAdminPanel() { document.getElementById('adminPanel').classList.add('hidden'); }
        
        function clearSystemData() {
            if(confirm("¿Estás seguro de reiniciar todo? Se perderán candidatos y votos permanentemente.")) {
                localStorage.clear();
                location.reload();
            }
        }

        function showToast(text, error = false) {
            const t = document.getElementById('toast');
            t.innerText = text;
            t.className = `fixed top-10 left-1/2 -translate-x-1/2 px-10 py-4 rounded-full text-[10px] font-black shadow-2xl z-[100] uppercase tracking-widest transition-all ${error ? 'bg-red-900 text-white' : 'bg-white text-black'}`;
            t.classList.remove('hidden');
            setTimeout(() => t.classList.add('hidden'), 3000);
        }

        // INICIALIZACIÓN
        refreshUI();
    </script>
</body>
</html>
