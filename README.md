class Mensagem {
    protected String campanha;
    protected int quantidade;

    public Mensagem(String campanha, int quantidade) {
        this.campanha = campanha;
        this.quantidade = quantidade;
    }

    // Método com retorno
    public double calcularCusto() {
        return 0.0;
    }

    // Método com retorno
    public String getCanal() {
        return "Mensagem";
    }

    // Método void
    public void exibirResumo() {
        System.out.printf(
            "%s | %s | %d envios | R$ %.2f%n",
            getCanal(),
            campanha,
            quantidade,
            calcularCusto()
        );
    }
}


class Email extends Mensagem {

    public Email(String campanha, int quantidade) {
        super(campanha, quantidade);
    }

    @Override
    public double calcularCusto() {
        double custo = quantidade * 0.02;

        if (quantidade > 1000) {
            custo = custo * 0.90;
        } else {
            custo = custo;
        }

        return custo;
    }

    @Override
    public String getCanal() {
        return "E-mail";
    }
}


class SMS extends Mensagem {

    public SMS(String campanha, int quantidade) {
        super(campanha, quantidade);
    }

    @Override
    public double calcularCusto() {
        return quantidade * 0.15;
    }

    @Override
    public String getCanal() {
        return "SMS";
    }
}


public class Main {

    public static void main(String[] args) {

        // Vetor do tipo Mensagem contendo Email e SMS
        Mensagem[] mensagens = {
            new Email("boas-vindas", 2500),
            new Email("promocao-agosto", 800),
            new SMS("codigo-verificacao", 300)
        };

        double total = 0.0;

        // Percorre o vetor
        for (Mensagem mensagem : mensagens) {
            mensagem.exibirResumo();
            total += mensagem.calcularCusto();
        }

        // Mostra o total
        System.out.printf("TOTAL DA FATURA: R$ %.2f%n", total);

        // Verifica o limite
        if (total > 100.00) {
            System.out.println("Atencao: fatura acima do limite contratado.");
        } else {
            System.out.println("Fatura dentro do limite.");
        }
    }
}
