import React, { useState, useMemo } from 'react';
import { Search, Film, Sparkles, Sliders, Heart, Play, Globe, CheckCircle } from 'lucide-react';

// Premium Curated International 4K / High-Quality Dataset
const MOVIE_DATABASE = [
  {
    id: 1,
    title: "Parasite",
    originalTitle: "기생충 (Gisaengchung)",
    country: "South Korea",
    year: "2019",
    quality: "4K Ultra HD",
    rating: "8.6",
    genre: "Thriller / Drama",
    description: "Greed and class discrimination threaten the newly formed symbiotic relationship between the wealthy Park family and the destitute Kim clan.",
    coverUrl: "https://images.unsplash.com/photo-1594909122845-11baa439b7bf?auto=format&fit=crop&q=80&w=600",
    backdropUrl: "https://images.unsplash.com/photo-1536440136628-849c177e76a1?auto=format&fit=crop&q=80&w=1200",
    is4K: true,
  },
  {
    id: 2,
    title: "Portrait of a Lady on Fire",
    originalTitle: "Portrait de la jeune fille en feu",
    country: "France",
    year: "2019",
    quality: "4K Dolby Vision",
    rating: "8.1",
    genre: "Romance / Drama",
    description: "On an isolated island in Brittany at the end of the eighteenth century, a female painter is obliged to paint a wedding portrait of a young woman.",
    coverUrl: "https://images.unsplash.com/photo-1485846234645-a62644f84728?auto=format&fit=crop&q=80&w=600",
    is4K: true,
  },
  {
    id: 3,
    title: "Spirited Away",
    originalTitle: "千と千尋の神隠し (Sen to Chihiro no Kamikakushi)",
    country: "Japan",
    year: "2001",
    quality: "4K Remastered",
    rating: "8.6",
    genre: "Animation / Fantasy",
    description: "During her family's move to the suburbs, a sullen 10-year-old girl wanders into a world ruled by gods, witches, and spirits, and where humans are changed into beasts.",
    coverUrl: "https://images.unsplash.com/photo-1578632767115-351597cf2477?auto=format&fit=crop&q=80&w=600",
    is4K: true,
  },
  {
    id: 4,
    title: "Another Round",
    originalTitle: "Druk",
    country: "Denmark",
    year: "2020",
    quality: "1080p Bluray",
    rating: "7.7",
    genre: "Drama / Comedy",
    description: "Four high-school teachers consume alcohol on a daily basis to see how it affects their social and professional lives.",
    coverUrl: "https://images.unsplash.com/photo-1513151233558-d860c5398176?auto=format&fit=crop&q=80&w=600",
    is4K: false,
  },
  {
    id: 5,
    title: "Pan's Labyrinth",
    originalTitle: "El laberinto del fauno",
    country: "Spain",
    year: "2006",
    quality: "4K Ultra HD",
    rating: "8.2",
    genre: "Fantasy / Drama",
    description: "In the Falangist Spain of 1944, the young stepdaughter of a sadistic army officer takes refuge in a eerie but captivating fantasy world.",
    coverUrl: "https://images.unsplash.com/photo-1618005182384-a83a8bd57fbe?auto=format&fit=crop&q=80&w=600",
    is4K: true,
  }
];

export default function App() {
  const [searchQuery, setSearchQuery] = useState("");
  const [activeTab, setActiveTab] = useState("all"); // all, 4k, international
  const [favorites, setFavorites] = useState({});
  const [selectedMovie, setSelectedMovie] = useState(MOVIE_DATABASE[0]);

  const toggleFavorite = (id) => {
    setFavorites(prev => ({ ...prev, [id]: !prev[id] }));
  };

  const filteredMovies = useMemo(() => {
    return MOVIE_DATABASE.filter(movie => {
      const matchesSearch = movie.title.toLowerCase().includes(searchQuery.toLowerCase()) || 
                            movie.originalTitle.toLowerCase().includes(searchQuery.toLowerCase());
      
      if (!matchesSearch) return false;
      if (activeTab === "4k") return movie.is4K;
      if (activeTab === "international") return movie.country !== "United States";
      return true;
    });
  }, [searchQuery, activeTab]);

  return (
    <div className="min-h-screen bg-[#0a0a0c] text-slate-100 font-sans antialiased selection:bg-amber-500 selection:text-black">
      {/* Top Elegant Navbar */}
      <nav className="sticky top-0 z-50 border-b border-white/5 bg-[#0a0a0c]/80 backdrop-blur-xl px-6 py-4 flex items-center justify-between">
        <div className="flex items-center gap-2 tracking-[0.2em] font-light text-lg uppercase text-white">
          <Sparkles className="w-5 h-5 text-amber-400 stroke-[1.5]" />
          <span>Aura<span className="font-semibold text-amber-400">Cinema</span></span>
        </div>

        {/* Global Navigation Controls */}
        <div className="flex items-center gap-8 text-sm tracking-wider uppercase font-medium">
          <button 
            onClick={() => setActiveTab("all")} 
            className={`transition-colors ${activeTab === "all" ? "text-amber-400" : "text-slate-400 hover:text-white"}`}
          >
            All Curations
          </button>
          <button 
            onClick={() => setActiveTab("4k")} 
            className={`transition-colors ${activeTab === "4k" ? "text-amber-400" : "text-slate-400 hover:text-white"}`}
          >
            4K Mastering
          </button>
          <button 
            onClick={() => setActiveTab("international")} 
            className={`transition-colors ${activeTab === "international" ? "text-amber-400" : "text-slate-400 hover:text-white"}`}
          >
            World Cinema
          </button>
        </div>

        {/* Interactive Search Bar */}
        <div className="relative w-64">
          <Search className="absolute left-3 top-2.5 w-4 h-4 text-slate-500" />
          <input 
            type="text" 
            placeholder="Search original titles..." 
            value={searchQuery}
            onChange={(e) => setSearchQuery(e.target.value)}
            className="w-full bg-white/5 border border-white/10 rounded-full pl-9 pr-4 py-2 text-xs tracking-wide focus:outline-none focus:border-amber-400/50 transition-all placeholder:text-slate-500 text-slate-200"
          />
        </div>
      </nav>

      {/* Cinematic Hero Segment */}
      <div className="relative h-[480px] w-full overflow-hidden flex items-end">
        <div className="absolute inset-0 bg-cover bg-center transition-all duration-700 filter brightness-50" style={{ backgroundImage: `url(${selectedMovie.backdropUrl || selectedMovie.coverUrl})` }}></div>
        <div className="absolute inset-0 bg-gradient-to-t from-[#0a0a0c] via-[#0a0a0c]/40 to-transparent"></div>
        
        <div className="relative max-w-4xl px-12 pb-12 z-10 space-y-4">
          <div className="flex items-center gap-3">
            <span className="bg-amber-400/10 text-amber-400 text-[10px] tracking-widest uppercase font-semibold px-2.5 py-1 rounded border border-amber-400/20 backdrop-blur-md">
              {selectedMovie.quality}
            </span>
            <span className="flex items-center gap-1 text-xs text-slate-300 font-medium">
              <Globe className="w-3.5 h-3.5 text-slate-400" /> {selectedMovie.country}
            </span>
          </div>
          <h1 className="text-4xl font-light tracking-tight text-white md:text-5xl">
            {selectedMovie.title}
          </h1>
          <p className="text-sm italic text-amber-200/60 font-serif tracking-wide">
            Original: {selectedMovie.originalTitle}
          </p>
          <p className="text-sm text-slate-300 max-w-2xl font-light leading-relaxed">
            {selectedMovie.description}
          </p>
          
          <div className="pt-2 flex items-center gap-4">
            <button 
              onClick={() => alert(`Launching Stream Framework for: ${selectedMovie.title}. Media link validated at 4K resolution.`)}
              className="flex items-center gap-2 bg-white text-black text-xs uppercase font-semibold tracking-wider px-6 py-3 rounded hover:bg-amber-400 transition-colors shadow-lg"
            >
              <Play className="w-4 h-4 fill-current" /> Watch Original Source
            </button>
            <button 
              onClick={() => toggleFavorite(selectedMovie.id)}
              className="p-3 bg-white/5 border border-white/10 rounded hover:bg-white/10 transition-colors"
            >
              <Heart className={`w-4 h-4 ${favorites[selectedMovie.id] ? "fill-amber-400 stroke-amber-400" : "text-white"}`} />
            </button>
          </div>
        </div>
      </div>

      {/* Main Grid / Content Showcase */}
      <main className="px-12 py-12 max-w-7xl mx-auto space-y-8">
        <div className="flex items-center justify-between border-b border-white/5 pb-4">
          <h2 className="text-lg uppercase tracking-[0.15em] font-light text-slate-300 flex items-center gap-2">
            <Film className="w-4 h-4 text-amber-500" /> Curated Masterpieces ({filteredMovies.length})
          </h2>
          <div className="flex items-center gap-2 text-xs text-slate-400">
            <Sliders className="w-3.5 h-3.5" /> Sorting: High Fidelity Quality Standard
          </div>
        </div>

        {filteredMovies.length === 0 ? (
          <div className="text-center py-20 border border-dashed border-white/5 rounded-xl bg-white/[0.01]">
            <p className="text-slate-400 font-light tracking-wide text-sm">No original high-fidelity films match your active filters.</p>
          </div>
        ) : (
          <div className="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 xl:grid-cols-5 gap-6">
            {filteredMovies.map((movie) => (
              <div 
                key={movie.id}
                onClick={() => setSelectedMovie(movie)}
                className={`group relative bg-white/[0.02] border rounded-lg overflow-hidden cursor-pointer transition-all duration-300 hover:translate-y-[-4px] hover:bg-white/[0.04] ${selectedMovie.id === movie.id ? "border-amber-400/40 shadow-xl shadow-amber-950/20" : "border-white/5"}`}
              >
                {/* Image Wrap */}
                <div className="aspect-[2/3] w-full overflow-hidden relative bg-slate-900">
                  <img 
                    src={movie.coverUrl} 
                    alt={movie.title}
                    className="w-full h-full object-cover transition-transform duration-500 group-hover:scale-105"
                    loading="lazy"
                  />
                  <div className="absolute inset-0 bg-gradient-to-t from-black/80 via-transparent to-transparent opacity-60 group-hover:opacity-40 transition-opacity"></div>
                  
                  {/* Absolute Quality Pill */}
                  <span className="absolute top-3 left-3 bg-black/70 backdrop-blur-md text-[9px] font-semibold text-amber-400 tracking-wider px-2 py-0.5 rounded border border-white/10">
                    {movie.is4K ? "4K" : "HD"}
                  </span>

                  {/* Absolute Favorite Toggle */}
                  <button 
                    onClick={(e) => {
                      e.stopPropagation();
                      toggleFavorite(movie.id);
                    }}
                    className="absolute top-3 right-3 p-2 bg-black/60 backdrop-blur-md rounded-full border border-white/5 opacity-0 group-hover:opacity-100 transition-opacity hover:bg-black/80"
                  >
                    <Heart className={`w-3.5 h-3.5 ${favorites[movie.id] ? "fill-amber-400 stroke-amber-400" : "text-slate-300"}`} />
                  </button>
                </div>

                {/* Text Block details */}
                <div className="p-4 space-y-1.5">
                  <div className="flex items-center justify-between text-[11px] text-slate-400 tracking-wide">
                    <span>{movie.country}</span>
                    <span>{movie.year}</span>
                  </div>
                  <h3 className="font-medium text-sm text-white tracking-wide truncate group-hover:text-amber-400 transition-colors">
                    {movie.title}
                  </h3>
                  <p className="text-[11px] font-serif italic text-slate-400 tracking-wide truncate">
                    {movie.originalTitle}
                  </p>
                  
                  <div className="pt-2 flex items-center justify-between border-t border-white/5 text-[11px]">
                    <span className="text-slate-500">{movie.genre.split(" / ")[0]}</span>
                    <span className="text-amber-400 font-medium">★ {movie.rating}</span>
                  </div>
                </div>
              </div>
            ))}
          </div>
        )}
      </main>

      {/* Minimal Footer */}
      <footer className="border-t border-white/5 mt-20 py-8 px-12 text-center text-xs text-slate-600 tracking-widest uppercase">
        © 2026 Aura Cinema. Stream architecture linked via globally authenticated networks.
      </footer>
    </div>
  );
}