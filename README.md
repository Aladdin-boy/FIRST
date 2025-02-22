# FIRST
JUST FOR TEST
import React, { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { ShoppingCart } from "lucide-react";

const products = [
  { id: 1, name: "Formation en Cloud", price: 999, details: "Apprenez le cloud computing." },
  { id: 2, name: "Formation en Cybersécurité", price: 1299, details: "Maîtrisez la cybersécurité." },
  { id: 3, name: "Formation en IA", price: 1499, details: "Devenez expert en intelligence artificielle." },
];

export default function Ecommerce() {
  const [cart, setCart] = useState([]);
  const [form, setForm] = useState({ name: "", numero: "", address: "", email: "" });

  const addToCart = (product) => {
    setCart([...cart, product]);
  };

  const handleChange = (e) => {
    setForm({ ...form, [e.target.name]: e.target.value });
  };

  return (
    <div className="p-6">
      <h1 className="text-3xl font-bold mb-4">Achetez vos Formations et Produits</h1>
      <div className="grid grid-cols-3 gap-4">
        {products.map((product) => (
          <Card key={product.id} className="p-4 shadow-lg">
            <CardContent>
              <h2 className="text-xl font-semibold">{product.name}</h2>
              <p className="text-gray-500">{product.price} MAD</p>
              <p className="text-sm text-gray-600">{product.details}</p>
              <Button className="mt-2" onClick={() => addToCart(product)}>
                Ajouter au panier
              </Button>
            </CardContent>
          </Card>
        ))}
      </div>
      <div className="mt-6 p-4 bg-gray-100 rounded-lg">
        <h2 className="text-2xl font-semibold flex items-center">
          <ShoppingCart className="mr-2" /> Panier
        </h2>
        {cart.length === 0 ? (
          <p className="text-gray-500">Votre panier est vide.</p>
        ) : (
          <ul>
            {cart.map((item, index) => (
              <li key={index} className="border-b py-2">
                {item.name} - {item.price} MAD
              </li>
            ))}
          </ul>
        )}
        <div className="mt-4">
          <h2 className="text-xl font-semibold">Informations Client</h2>
          <Input name="name" placeholder="Nom" onChange={handleChange} className="mb-2" />
          <Input name="numero" placeholder="Numéro de téléphone" onChange={handleChange} className="mb-2" />
          <Input name="address" placeholder="Adresse" onChange={handleChange} className="mb-2" />
          <Input name="email" placeholder="Email" type="email" onChange={handleChange} className="mb-2" />
          <Button className="mt-4 w-full">Passer la commande</Button>
        </div>
      </div>
    </div>
  );
}
