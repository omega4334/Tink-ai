# Tink-ai 
git add .
git commit -m "Initial commit"
import React, { useState } from "react"; import { Input } from "@/components/ui/input"; import { Button } from "@/components/ui/button"; import { Card, CardContent } from "@/components/ui/card"; import { motion } from "framer-motion";

export default function SmartAI() { const [input, setInput] = useState(""); const [response, setResponse] = useState(""); const [loading, setLoading] = useState(false);

const askAI = async () => { if (!input.trim()) return; setLoading(true); setResponse(""); try { const res = await fetch("/api/ask", { method: "POST", headers: { "Content-Type": "application/json" }, body: JSON.stringify({ question: input }), }); const data = await res.json(); setResponse(data.answer); } catch (err) { setResponse("Error talking to AI."); } setLoading(false); };

return ( <div className="min-h-screen bg-gray-100 p-4 grid place-items-center"> <Card className="w-full max-w-2xl shadow-xl rounded-2xl"> <CardContent className="p-6 space-y-4"> <h1 className="text-3xl font-bold text-center">Super Reasoning AI</h1> <Input value={input} onChange={(e) => setInput(e.target.value)} placeholder="Ask me anything..." className="text-lg" /> <Button onClick={askAI} disabled={loading} className="w-full"> {loading ? "Thinking..." : "Ask"} </Button> {response && ( <motion.div initial={{ opacity: 0 }} animate={{ opacity: 1 }} className="bg-white p-4 rounded-xl shadow-inner text-gray-800" > {response} </motion.div> )} </CardContent> </Card> </div> ); }

