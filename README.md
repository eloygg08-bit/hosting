import React, { useState, useEffect } from 'react';
import { Camera, Code, Palette, Github, Mail, Linkedin } from 'lucide-react';

export default function ModernPortfolio() {
  const [currentImage, setCurrentImage] = useState(0);
  const [userName, setUserName] = useState('Visitante');
  const [displayName, setDisplayName] = useState('Visitante');
  const [ballPosition, setBallPosition] = useState({ x: 50, y: 50 });
  const [ballVelocity, setBallVelocity] = useState({ x: 2, y: 1.5 });

  // Imágenes para el intercambio
  const images = [
    { url: 'https://images.unsplash.com/photo-1517694712202-14dd9538aa97?w=800', alt: 'Código en pantalla' },
    { url: 'https://images.unsplash.com/photo-1498050108023-c5249f4df085?w=800', alt: 'Desarrollo web' },
    { url: 'https://images.unsplash.com/photo-1461749280684-dccba630e2f6?w=800', alt: 'Programación' }
  ];

  // Animación del objeto en movimiento
  useEffect(() => {
    const interval = setInterval(() => {
      setBallPosition(prev => {
        let newX = prev.x + ballVelocity.x;
        let newY = prev.y + ballVelocity.y;
        let newVelX = ballVelocity.x;
        let newVelY = ballVelocity.y;

        if (newX <= 0 || newX >= 95) {
          newVelX = -newVelX;
          newX = newX <= 0 ? 0 : 95;
        }
        if (newY <= 0 || newY >= 95) {
          newVelY = -newVelY;
          newY = newY <= 0 ? 0 : 95;
        }

        setBallVelocity({ x: newVelX, y: newVelY });
        return { x: newX, y: newY };
      });
    }, 30);

    return () => clearInterval(interval);
  }, [ballVelocity]);

  const handleImageClick = () => {
    setCurrentImage((prev) => (prev + 1) % images.length);
  };

  const handleNameSubmit = (e) => {
    e.preventDefault();
    setDisplayName(userName || 'Visitante');
  };

  return (
    <div className="min-h-screen bg-gradient-to-br from-slate-900 via-purple-900 to-slate-900 text-white relative overflow-hidden">
      {/* Objeto en movimiento */}
      <div
        className="absolute w-16 h-16 bg-gradient-to-br from-cyan-400 to-blue-500 rounded-full shadow-lg shadow-cyan-500/50 transition-all duration-75 pointer-events-none"
        style={{
          left: `${ballPosition.x}%`,
          top: `${ballPosition.y}%`,
          boxShadow: '0 0 40px rgba(34, 211, 238, 0.6)'
        }}
      />

      {/* Header */}
      <header className="relative z-10 p-8 backdrop-blur-sm bg-white/5 border-b border-white/10">
        <nav className="max-w-6xl mx-auto flex justify-between items-center">
          <h1 className="text-3xl font-bold bg-gradient-to-r from-cyan-400 to-purple-400 bg-clip-text text-transparent" style={{ fontFamily: 'Orbitron, sans-serif' }}>
            DevPortfolio
          </h1>
          <div className="flex gap-6">
            <a href="#" className="hover:text-cyan-400 transition-colors"><Github size={24} /></a>
            <a href="#" className="hover:text-cyan-400 transition-colors"><Linkedin size={24} /></a>
            <a href="#" className="hover:text-cyan-400 transition-colors"><Mail size={24} /></a>
          </div>
        </nav>
      </header>

      {/* Hero Section */}
      <section className="relative z-10 max-w-6xl mx-auto px-8 py-20">
        <div className="text-center mb-16">
          <h2 className="text-6xl font-bold mb-6" style={{ fontFamily: 'Orbitron, sans-serif' }}>
            Hola, <span className="bg-gradient-to-r from-cyan-400 via-purple-400 to-pink-400 bg-clip-text text-transparent">{displayName}</span>
          </h2>
          <p className="text-xl text-gray-300 mb-8">Desarrollo web creativo e interactivo</p>
          
          {/* Campo de texto interactivo */}
          <div className="max-w-md mx-auto mb-12">
            <div className="flex gap-3">
              <input
                type="text"
                value={userName}
                onChange={(e) => setUserName(e.target.value)}
                onKeyPress={(e) => e.key === 'Enter' && handleNameSubmit(e)}
                placeholder="Introduce tu nombre..."
                className="flex-1 px-6 py-3 rounded-full bg-white/10 border border-white/20 backdrop-blur-sm focus:outline-none focus:border-cyan-400 transition-all"
              />
              <button
                onClick={handleNameSubmit}
                className="px-8 py-3 rounded-full bg-gradient-to-r from-cyan-500 to-purple-500 hover:from-cyan-400 hover:to-purple-400 transition-all font-semibold shadow-lg hover:shadow-cyan-500/50"
              >
                Actualizar
              </button>
            </div>
          </div>
        </div>

        {/* Grid de características */}
        <div className="grid md:grid-cols-3 gap-8 mb-16">
          <div className="p-6 rounded-2xl bg-white/5 backdrop-blur-sm border border-white/10 hover:border-cyan-400/50 transition-all hover:transform hover:scale-105">
            <Code className="w-12 h-12 text-cyan-400 mb-4" />
            <h3 className="text-2xl font-bold mb-3">Desarrollo</h3>
            <p className="text-gray-300">Código limpio y eficiente con las últimas tecnologías</p>
          </div>
          
          <div className="p-6 rounded-2xl bg-white/5 backdrop-blur-sm border border-white/10 hover:border-purple-400/50 transition-all hover:transform hover:scale-105">
            <Palette className="w-12 h-12 text-purple-400 mb-4" />
            <h3 className="text-2xl font-bold mb-3">Diseño</h3>
            <p className="text-gray-300">Interfaces modernas y experiencias visuales impactantes</p>
          </div>
          
          <div className="p-6 rounded-2xl bg-white/5 backdrop-blur-sm border border-white/10 hover:border-pink-400/50 transition-all hover:transform hover:scale-105">
            <Camera className="w-12 h-12 text-pink-400 mb-4" />
            <h3 className="text-2xl font-bold mb-3">Interactividad</h3>
            <p className="text-gray-300">Animaciones fluidas y elementos dinámicos</p>
          </div>
        </div>

        {/* Galería interactiva */}
        <div className="max-w-2xl mx-auto">
          <h3 className="text-3xl font-bold text-center mb-8" style={{ fontFamily: 'Orbitron, sans-serif' }}>
            Galería Interactiva
          </h3>
          <p className="text-center text-gray-300 mb-6">Haz clic en la imagen para cambiarla</p>
          <div
            onClick={handleImageClick}
            className="relative rounded-2xl overflow-hidden cursor-pointer group shadow-2xl shadow-purple-500/20 hover:shadow-purple-500/40 transition-all"
          >
            <img
              src={images[currentImage].url}
              alt={images[currentImage].alt}
              className="w-full h-96 object-cover group-hover:scale-110 transition-transform duration-500"
            />
            <div className="absolute inset-0 bg-gradient-to-t from-black/60 to-transparent opacity-0 group-hover:opacity-100 transition-opacity flex items-end justify-center pb-8">
              <p className="text-xl font-semibold">Clic para cambiar imagen ({currentImage + 1}/{images.length})</p>
            </div>
          </div>
        </div>
      </section>

      {/* Footer */}
      <footer className="relative z-10 mt-20 p-8 backdrop-blur-sm bg-white/5 border-t border-white/10">
        <div className="max-w-6xl mx-auto text-center text-gray-400">
          <p className="mb-2">© 2024 DevPortfolio - Proyecto Web Interactivo</p>
          <p className="text-sm">Licencia Creative Commons BY-NC-SA 4.0</p>
          <p className="text-xs mt-2">Diseño inspirado en portfolios modernos con glassmorphism</p>
        </div>
      </footer>

      {/* Estilos para la fuente */}
      <style>{`
        @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&display=swap');
      `}</style>
    </div>
  );
}
