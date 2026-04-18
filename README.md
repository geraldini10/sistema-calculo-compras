import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);

        double valor, total, frete, juros, desconto;
        int tipoCliente, pagamento, parcelas, itens, mes;
        String  aniversario, temCupom;

        //Inicialização
        desconto = 0;
        frete = 0;
        juros = 0;
        parcelas = 0;
        temCupom = null;
        pagamento = 0;
        aniversario = null;

            //entradas
            System.out.println("=== Sistema de calcular compras");
            System.out.println("Digite o valor da compra: ");
            valor = input.nextDouble();
            System.out.println("Tipo de cliente: ");
            System.out.println("1 > COMUM");
            System.out.println("2 > VIP");
            System.out.println("3 > PREMIUM");
            tipoCliente = input.nextInt();

            //formas de pagamento
            System.out.println("Qual a forma de pagamento?: ");
            System.out.println("1 > À vista (Pix/Dinheiro");
            System.out.println("2 > Cartão de débito");
            System.out.println("3 > Cartão de crédito");
            pagamento = input.nextInt();

            if(pagamento == 3){
            System.out.println("Número de parcelas (1 a 12)");
            parcelas = input.nextInt();
        }
        System.out.println("Quantidades de itens comprados: ");
            itens = input.nextInt();
        System.out.println("Mês da compra: ");
        mes = input.nextInt();
        System.out.println("Aniversário no mês?: ");
        aniversario = input.next();
        System.out.println("Tem cupom promocional?: ");
        temCupom = input.next();

        //regras de desconto por taxa de valor
        if(valor <=200){
            desconto = 5.0;
        }else if(valor <=800){
            desconto = 12.0;
        }else if(valor <=2000.0){
            desconto = 18.0;
        }else{
            desconto = 22.0;
        }
        //descontos cumulativos
        if(tipoCliente ==2){
            desconto = desconto +5.0;
        }
        if(tipoCliente ==3){
            desconto = desconto +8.0;
        }
        if(pagamento ==1){
            desconto = desconto +3.0;
        }
        if(pagamento ==2){
            desconto = desconto +1.0;
        }
        if(itens >=10){
            desconto = desconto +4.0;
        }
        if(aniversario.equals("S") || aniversario.equals("s")){
            desconto = desconto +2.0;
        }
        if(mes == 6 || mes == 12){
            desconto = desconto +3.0;
        }

        //cupons
        if(temCupom.equals("BEMVINDO10")){
            if(tipoCliente ==1){
                desconto = desconto +10.0;
            }else{
                System.out.println("AVISO: Cupom BEMVINDO10 válido apenas para cliente Comuns.");
            }
        }
        if(temCupom.equals("SUPER15")){
            if(valor > 500){
                desconto = desconto +15.0;
            }else{
                System.out.println("AVISO, Cupom SUPER15 exige compra acima de R$500,00.");
            }
        }

        //aplicando desconto
        total = valor - (valor * desconto /100.0);

        //frete
        if(valor <150){
            frete = 25.0;
        }else if(valor < 500.0){
            frete = 15.0;
        }
        if(temCupom.equals("FRETE0")){
            frete = 0.0;
        }

        //juros de parcelamento

        if(pagamento == 3){
            if(parcelas <=3){
                juros = 0.0;
            }else if(parcelas >= 4 && parcelas <=6){
                juros = total *0.02;
            }else if(parcelas >=7 && parcelas <=9){
                juros = total *0.04;
            }else if(parcelas <=12){
                juros = total *0.07;
            }
        }

        total = total + frete + juros;

        //saida
        System.out.println("=======================");
        System.out.println("Valor original: R$ "+ valor);
        System.out.println("Desconto total: "+desconto + "%");
        System.out.println("Economia: R$ "+ (valor * desconto /100.0));

        if(juros >0.0){
            System.out.println("Juros: R$ "+juros);
        }else{
            System.out.println("Sem juros");
        }if(frete >0.0){
            System.out.println("Frete: R$ "+frete);
        }else{
            System.out.println("Frete: Grátis");
        }

        System.out.println("============");
        System.out.println("Valor final: R$ "+ total);

        if(pagamento == 3 && parcelas > 1){
            System.out.println("Parcelado em: "+parcelas+ "x de R$"+ (total / parcelas));
        }

    }
}
