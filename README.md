import { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { LineChart, Line, XAxis, YAxis, Tooltip, ResponsiveContainer } from "recharts";
import Sidebar from "../components/Sidebar"; // Adjusted import path

const sampleBots = [
  {
    id: 1,
    name: "Bot Scalping EUR/USD",
    status: "Running",
    profit: 1200,
    risk: "Medium",
    performance: [
      { time: "Day 1", value: 200 },
      { time: "Day 2", value: 500 },
      { time: "Day 3", value: 800 },
      { time: "Day 4", value: 1200 },
    ],
  },
  {
    id: 2,
    name: "Bot Trend Following GBP/USD",
    status: "Stopped",
    profit: 800,
    risk: "Low",
    performance: [
      { time: "Day 1", value: 100 },
      { time: "Day 2", value: 300 },
      { time: "Day 3", value: 600 },
      { time: "Day 4", value: 800 },
    ],
  },
];

export default function Dashboard() {
  const [bots, setBots] = useState(sampleBots);

  return (
    <div className="flex h-screen">
      <Sidebar />
      <div className="flex-1 p-6">
        <h1 className="text-2xl font-bold mb-4">Dashboard Bot Giao Dịch</h1>
        <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
          {bots.map((bot) => (
            <Card key={bot.id} className="p-4">
              <h2 className="text-xl font-semibold">{bot.name}</h2>
              <p className={`text-sm ${bot.status === "Running" ? "text-green-500" : "text-red-500"}`}>{bot.status}</p>
              <p className="text-sm">Lợi nhuận: ${bot.profit}</p>
              <p className="text-sm">Rủi ro: {bot.risk}</p>
              <ResponsiveContainer width="100%" height={100}>
                <LineChart data={bot.performance}>
                  <XAxis dataKey="time" hide />
                  <YAxis hide />
                  <Tooltip />
                  <Line type="monotone" dataKey="value" stroke="#8884d8" strokeWidth={2} />
                </LineChart>
              </ResponsiveContainer>
              <Button className="mt-2" variant="outline">
                {bot.status === "Running" ? "Dừng Bot" : "Khởi Động Bot"}
              </Button>
            </Card>
          ))}
        </div>
      </div>
    </div>
  );
}
