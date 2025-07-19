import { useState } from "react";

const App = () => {
  const [activePage, setActivePage] = useState("home");
  const [form, setForm] = useState({
    name: "",
    email: "",
    service: "",
    details: "",
  });

  const services = [
    { name: "T-Shirt Printing", price: "R150" },
    { name: "Business Cards", price: "R250" },
    { name: "Keychains", price: "R45" },
    { name: "Hoodies", price: "R300" },
    { name: "Car Branding", price: "R2000" },
    { name: "Mug Printing", price: "R90" },
    { name: "Embroidery", price: "R80" },
    { name: "Wedding Shawls", price: "R600" },
    { name: "Carvings", price: "R500" },
  ];

  const handleInputChange = (e) => {
    const { name, value } = e.target;
    setForm({ ...form, [name]: value });
  };

  const handleSubmit = (e) => {
    e.preventDefault();

    // Prepare WhatsApp message
    const phoneNumber = "0742867194";
    const message = `
*Modimolle Printers - Quote Request*

Name: ${encodeURIComponent(form.name)}
Email: ${encodeURIComponent(form.email)}
Service: ${encodeURIComponent(form.service)}
Details: ${encodeURIComponent(form.details)}
    `.trim();

    const whatsappUrl = `https://wa.me/ ${phoneNumber}?text=${message}`;

    // Open WhatsApp in new tab
    window.open(whatsappUrl, "_blank");

    // Optional: reset form after submission
    setForm({ name: "", email: "", service: "", details: "" });
  };

  return (
    <div className="min-h-screen bg-white text-gray-800">
      {/* Header */}
      <header className="bg-black text-white p-4 flex justify-between items-center shadow-md fixed w-full z-50">
        <h1 className="text-xl font-bold">Modimolle Printers</h1>
        <nav className="space-x-4 hidden md:flex">
          {["home", "services", "gallery", "pricing", "quote", "contact"].map((page) => (
            <button key={page} onClick={() => setActivePage(page)} className="hover:underline capitalize">
              {page}
            </button>
          ))}
        </nav>
        <button
          onClick={() => setActivePage("contact")}
          className="bg-green-500 hover:bg-green-600 px-4 py-2 rounded-md text-white"
        >
          Contact Us
        </button>
      </header>

      {/* Mobile Nav */}
      <div className="md:hidden fixed bottom-16 left-0 right-0 bg-white border-t shadow-lg z-50">
        <div className="flex justify-around py-2">
          {["home", "services", "gallery", "pricing", "quote", "contact"].map((page) => (
            <button
              key={page}
              onClick={() => setActivePage(page)}
              className={`capitalize ${activePage === page ? "text-blue-600 font-bold" : "text-gray-500"}`}
            >
              {page}
            </button>
          ))}
        </div>
      </div>

      {/* Main Content */}
      <main className="pt-20 pb-24">
        {/* Home Page */}
        {activePage === "home" && (
          <section className="px-4 py-12 text-center">
            <h2 className="text-3xl md:text-4xl font-extrabold mb-4 text-gray-900">
              Welcome to Modimolle Printers
            </h2>
            <p className="max-w-xl mx-auto text-lg mb-8 text-gray-700">
              Your one-stop solution for all printing needs in Modimolle. From t-shirts to car branding,
              we’ve got you covered.
            </p>
            <div className="grid grid-cols-2 md:grid-cols-3 gap-6">
              {["T-Shirts", "Business Cards", "Hoodies", "Mugs", "Embroidery", "Wedding Shawls"].map(
                (service) => (
                  <div
                    key={service}
                    className="bg-gray-100 p-4 rounded-lg shadow hover:shadow-xl transition-shadow"
                  >
                    <img
                      src={`https://placehold.co/300x200?text=${encodeURIComponent(service)}`}
                      alt={service}
                      className="w-full h-32 object-cover rounded"
                    />
                    <h3 className="mt-2 font-semibold">{service}</h3>
                  </div>
                )
              )}
            </div>
            <button
              onClick={() => setActivePage("quote")}
              className="mt-8 bg-blue-600 hover:bg-blue-700 text-white px-6 py-3 rounded-full shadow-lg transform transition-transform hover:scale-105"
            >
              Get a Quote
            </button>
          </section>
        )}

        {/* Services Page */}
        {activePage === "services" && (
          <section className="px-4 py-12">
            <h2 className="text-3xl font-bold text-center mb-8">Our Services</h2>
            <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
              {services.map((service, index) => (
                <div
                  key={index}
                  className="border rounded-lg overflow-hidden shadow hover:shadow-xl transition-shadow"
                >
                  <img
                    src={` https://placehold.co/400x250?text=${encodeURIComponent(service.name)}`}
                    alt={service.name}
                    className="w-full h-40 object-cover"
                  />
                  <div className="p-4">
                    <h3 className="font-semibold text-lg">{service.name}</h3>
                    <p className="text-sm text-gray-600">From {service.price}</p>
                  </div>
                </div>
              ))}
            </div>
          </section>
        )}

        {/* Gallery Page */}
        {activePage === "gallery" && (
          <section className="px-4 py-12">
            <h2 className="text-3xl font-bold text-center mb-8">Gallery</h2>
            <div className="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-4">
              {[
                "T-Shirt Design",
                "Custom Mug",
                "Car Branding",
                "Wedding Shawl",
                "Embroidery Sample",
                "Hoodie Mockup",
              ].map((item, i) => (
                <img
                  key={i}
                  src={` https://placehold.co/600x400?text=${encodeURIComponent(item)}`}
                  alt={item}
                  className="rounded shadow-md hover:shadow-xl transition-shadow"
                />
              ))}
            </div>
          </section>
        )}

        {/* Pricing Page */}
        {activePage === "pricing" && (
          <section className="px-4 py-12">
            <h2 className="text-3xl font-bold text-center mb-8">Pricing Catalog</h2>
            <div className="max-w-3xl mx-auto space-y-4">
              {services.map((service, i) => (
                <div
                  key={i}
                  className="flex justify-between items-center p-4 border rounded-lg bg-gray-50 hover:bg-gray-100"
                >
                  <span>{service.name}</span>
                  <span className="font-semibold">{service.price}</span>
                </div>
              ))}
            </div>
          </section>
        )}

        {/* Quote Form Page */}
        {activePage === "quote" && (
          <section className="px-4 py-12 max-w-2xl mx-auto">
            <h2 className="text-3xl font-bold text-center mb-8">Request a Quote</h2>
            <form onSubmit={handleSubmit} className="space-y-4">
              <input
                type="text"
                name="name"
                placeholder="Your Name"
                value={form.name}
                onChange={handleInputChange}
                required
                className="w-full p-3 border rounded-md"
              />
              <input
                type="email"
                name="email"
                placeholder="Email Address"
                value={form.email}
                onChange={handleInputChange}
                required
                className="w-full p-3 border rounded-md"
              />
              <select
                name="service"
                value={form.service}
                onChange={handleInputChange}
                required
                className="w-full p-3 border rounded-md"
              >
                <option value="">Select Service</option>
                {services.map((s, i) => (
                  <option key={i} value={s.name}>
                    {s.name}
                  </option>
                ))}
              </select>
              <textarea
                name="details"
                placeholder="Details of your request..."
                rows="4"
                value={form.details}
                onChange={handleInputChange}
                className="w-full p-3 border rounded-md"
              ></textarea>
              <button
                type="submit"
                className="w-full bg-blue-600 hover:bg-blue-700 text-white py-3 rounded-md font-semibold"
              >
                Submit Request via WhatsApp
              </button>
            </form>
          </section>
        )}

        {/* Contact Page */}
        {activePage === "contact" && (
          <section className="px-4 py-12 max-w-3xl mx-auto">
            <h2 className="text-3xl font-bold text-center mb-8">Contact Us</h2>
            <div className="bg-gray-100 p-6 rounded-lg shadow-inner">
              <p className="mb-4">
                <strong>Phone:</strong> 074 286 7194 / 065 243 7463
              </p>
              <p className="mb-4">
                <strong>Email:</strong> ModimollePrinters@gmail.com
              </p>
              <p className="mb-6">
                <strong>Shop Hours:</strong> 7am – 7pm
              </p>
              <a
                href=" https://wa.me/0742867194 "
                target="_blank"
                rel="noopener noreferrer"
                className="inline-block bg-green-500 hover:bg-green-600 text-white px-6 py-3 rounded-full mb-6"
              >
                Chat on WhatsApp
              </a>
              <div className="aspect-video w-full">
                <iframe
                  title="Google Maps - 59 Pretorius Street, Modimolle 0510"
                  src="https://www.google.com/maps?q=59+Pretorius+St,+Modimolle+0510&output=embed"
                  className="w-full h-full rounded"
                  allowFullScreen=""
                  loading="lazy"
                  referrerPolicy="no-referrer-when-downgrade"
                ></iframe>
              </div>
            </div>
          </section>
        )}
      </main>

      {/* Sticky WhatsApp Button with Chat Badge */}
      <div className="fixed bottom-20 right-6 z-50 flex items-center gap-2 animate-bounce">
        <a
          href=" https://wa.me/0742867194 "
          target="_blank"
          rel="noopener noreferrer"
          className="bg-green-500 hover:bg-green-600 text-white p-4 rounded-full shadow-lg"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="24"
            height="24"
            viewBox="0 0 24 24"
            fill="currentColor"
          >
            <path d="M20.1 3.9C17.9 1.7 15 .5 12 .5 5.8.5.7 5.6.7 11.9c0 2 .5 3.9 1.5 5.6L.6 23.4l6-1.6c1.6.9 3.5 1.3 5.4 1.3 6.3 0 11.4-5.1 11.4-11.4-.1-2.8-1.2-5.4-3.3-7.4zM12 21.4c-1.7 0-3.3-.5-4.8-1.3l-.3-.2-3.5 1 1-3.4L4 17c-1-1.5-1.4-3.2-1.4-5.1 0-5.2 4.2-9.4 9.4-9.4 2.5 0 4.9 1 6.7 2.8 1.8 1.8 2.8 4.2 2.8 6.7-.1 5.2-4.3 9.4-9.5 9.4zm7.1-7.1c-1.1 0-2-.9-2-2s.9-2 2-2 2 .9 2 2-.9 2-2 2z" />
          </svg>
        </a>
        <span className="bg-green-100 text-green-800 text-xs px-2 py-1 rounded-full font-semibold whitespace-nowrap">
          Chat Now!
        </span>
      </div>
    </div>
  );
};

export default App;
