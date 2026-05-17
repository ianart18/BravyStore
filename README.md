# BravyStore
Top up game termurah
import { useState } from 'react';

export default function TopUpGameTemplate() {
  const [userId, setUserId] = useState('');
  const [selectedGame, setSelectedGame] = useState('');
  const [selectedNominal, setSelectedNominal] = useState('');
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState('');

  const products = [
    { id: 1, name: "Mobile Legends", price: "86 Diamonds - Rp20.000" },
    { id: 2, name: "Free Fire", price: "140 Diamonds - Rp18.000" },
    { id: 3, name: "PUBG Mobile", price: "325 UC - Rp70.000" },
    { id: 4, name: "Honor of Kings", price: "80 Tokens - Rp15.000" },
  ];

  const paymentMethods = [
    "QRIS", "DANA", "OVO", "GoPay", 
    "BCA", "BNI", "BRI", "Mandiri"
  ];

  const handleBuyNow = async (e) => {
    e.preventDefault();
    
    // Validation
    if (!userId.trim()) {
      setError('Masukkan User ID');
      return;
    }
    if (!selectedGame) {
      setError('Pilih Game');
      return;
    }
    if (!selectedNominal) {
      setError('Pilih Nominal');
      return;
    }

    setError('');
    setLoading(true);
    
    try {
      // API call would go here
      console.log({ userId, selectedGame, selectedNominal });
      // await processTopUp({ userId, selectedGame, selectedNominal });
    } catch (err) {
      setError('Terjadi kesalahan. Silakan coba lagi.');
    } finally {
      setLoading(false);
    }
  };

  return (
    <div className="min-h-screen bg-gray-100 text-gray-900">
      {/* Header */}
      <header className="bg-blue-600 text-white p-5 shadow-lg">
        <div className="max-w-6xl mx-auto flex justify-between items-center">
          <h1 className="text-3xl font-bold">TopUp Diamond</h1>
          <button 
            className="bg-white text-blue-600 px-4 py-2 rounded-xl font-semibold hover:scale-105 transition"
            aria-label="Login to account"
          >
            Login
          </button>
        </div>
      </header>

      {/* Hero */}
      <section className="max-w-6xl mx-auto py-12 px-4 text-center">
        <h2 className="text-5xl font-bold mb-4">
          Top Up Game Murah & Instan
        </h2>
        <p className="text-lg text-gray-600 mb-8">
          Proses cepat, aman, dan tersedia berbagai pembayaran QRIS, Dana, OVO, dan Bank.
        </p>

        <form onSubmit={handleBuyNow} className="bg-white rounded-3xl shadow-xl p-6 max-w-2xl mx-auto">
          <div className="grid gap-4">
            <div>
              <label htmlFor="userId" className="block text-left text-sm font-semibold mb-2">
                User ID
              </label>
              <input
                id="userId"
                type="text"
                placeholder="Masukkan User ID"
                value={userId}
                onChange={(e) => setUserId(e.target.value)}
                className="w-full border border-gray-300 p-3 rounded-xl focus:outline-none focus:ring-2 focus:ring-blue-600"
              />
            </div>

            <div>
              <label htmlFor="game" className="block text-left text-sm font-semibold mb-2">
                Pilih Game
              </label>
              <select 
                id="game"
                value={selectedGame}
                onChange={(e) => setSelectedGame(e.target.value)}
                className="w-full border border-gray-300 p-3 rounded-xl focus:outline-none focus:ring-2 focus:ring-blue-600"
              >
                <option value="">Pilih Game</option>
                {products.map((product) => (
                  <option key={product.id} value={product.name}>
                    {product.name}
                  </option>
                ))}
              </select>
            </div>

            <div>
              <label htmlFor="nominal" className="block text-left text-sm font-semibold mb-2">
                Pilih Nominal
              </label>
              <select 
                id="nominal"
                value={selectedNominal}
                onChange={(e) => setSelectedNominal(e.target.value)}
                className="w-full border border-gray-300 p-3 rounded-xl focus:outline-none focus:ring-2 focus:ring-blue-600"
              >
                <option value="">Pilih Nominal</option>
                <option>86 Diamonds</option>
                <option>140 Diamonds</option>
                <option>325 UC</option>
              </select>
            </div>

            {error && <p className="text-red-600 text-sm">{error}</p>}

            <button 
              type="submit"
              disabled={loading}
              className="bg-blue-600 text-white py-3 rounded-xl text-lg font-bold hover:bg-blue-700 transition disabled:bg-gray-400 cursor-pointer"
            >
              {loading ? 'Processing...' : 'Beli Sekarang'}
            </button>
          </div>
        </form>
      </section>

      {/* Product Cards */}
      <section className="max-w-6xl mx-auto px-4 pb-16">
        <h3 className="text-3xl font-bold mb-6">Produk Populer</h3>
        <div className="grid md:grid-cols-2 lg:grid-cols-4 gap-6">
          {products.map((item) => (
            <div
              key={item.id}
              className="bg-white rounded-3xl shadow-lg p-5 hover:scale-105 transition"
            >
              <div className="h-32 bg-gray-200 rounded-2xl mb-4 flex items-center justify-center text-gray-500">
                Gambar Game
              </div>
              <h4 className="text-xl font-bold mb-2">{item.name}</h4>
              <p className="text-gray-600 mb-4">{item.price}</p>
              <button 
                className="w-full bg-blue-600 text-white py-2 rounded-xl font-semibold hover:bg-blue-700 transition"
                aria-label={`Top up ${item.name}`}
              >
                Top Up
              </button>
            </div>
          ))}
        </div>
      </section>

      {/* Payment */}
      <section className="bg-white py-12">
        <div className="max-w-6xl mx-auto px-4 text-center">
          <h3 className="text-3xl font-bold mb-8">Metode Pembayaran</h3>
          <div className="grid grid-cols-2 md:grid-cols-4 gap-4">
            {paymentMethods.map((pay) => (
              <div
                key={pay}
                className="bg-gray-100 rounded-2xl p-5 font-bold shadow"
              >
                {pay}
              </div>
            ))}
          </div>
        </div>
      </section>

      {/* Footer */}
      <footer className="bg-gray-900 text-white py-8 mt-10">
        <div className="max-w-6xl mx-auto px-4 text-center">
          <p className="text-lg font-semibold">© 2026 TopUp Diamond</p>
          <p className="text-gray-400 mt-2">
            Website top up game otomatis dan terpercaya.
          </p>
        </div>
      </footer>
    </div>
  );
}
