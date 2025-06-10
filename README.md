import { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Input } from "@/components/ui/input";
import { Button } from "@/components/ui/button";

export default function ConsigView() {
  const [cpf, setCpf] = useState("");
  const [senha, setSenha] = useState("");
  const [loading, setLoading] = useState(false);
  const [dados, setDados] = useState(null);

  const handleConsulta = () => {
    setLoading(true);
    setTimeout(() => {
      // Mock de dados simulando resultado do IN100
      setDados({
        nome: "João da Silva",
        beneficio: "123.456.789-0",
        banco: "Banco do Brasil",
        margemDisponivel: "R$ 1.233,45",
        contratos: [
          { banco: "Itaú", parcela: "R$ 255,00", saldo: "R$ 4.590,00", parcelas: 18 },
          { banco: "C6 Bank", parcela: "R$ 198,00", saldo: "R$ 2.178,00", parcelas: 12 },
        ],
      });
      setLoading(false);
    }, 2000);
  };

  return (
    <div className="p-4 max-w-2xl mx-auto space-y-4">
      <h1 className="text-3xl font-bold text-center mb-4">ConsigView</h1>

      <Card>
        <CardContent className="space-y-4 p-6">
          <Input
            placeholder="Digite o CPF"
            value={cpf}
            onChange={(e) => setCpf(e.target.value)}
          />
          <Input
            placeholder="Senha gov.br"
            type="password"
            value={senha}
            onChange={(e) => setSenha(e.target.value)}
          />
          <Button onClick={handleConsulta} disabled={loading}>
            {loading ? "Consultando..." : "Consultar IN100"}
          </Button>
        </CardContent>
      </Card>

      {dados && (
        <Card>
          <CardContent className="space-y-3 p-6">
            <h2 className="text-xl font-semibold">Dados do Beneficiário</h2>
            <p><strong>Nome:</strong> {dados.nome}</p>
            <p><strong>Benefício:</strong> {dados.beneficio}</p>
            <p><strong>Banco Pagador:</strong> {dados.banco}</p>
            <p><strong>Margem Disponível:</strong> {dados.margemDisponivel}</p>

            <h3 className="mt-4 font-semibold">Contratos Ativos:</h3>
            <ul className="list-disc pl-5">
              {dados.contratos.map((c, i) => (
                <li key={i}>
                  {c.banco} - {c.parcela} por {c.parcelas}x (Saldo: {c.saldo})
                </li>
              ))}
            </ul>
          </CardContent>
        </Card>
      )}
    </div>
  );
}
