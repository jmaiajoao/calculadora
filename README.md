# calculadora PSC

class Professor {
    constructor(nome, regime) {
        this.nome = nome;
        this.regime = regime;
        this.salarioMensal = 0;
        this.horasTrabalhadas = 0;
        this.valorHora = 0;
        this.valorContrato = 0;
    }

    calcularValorAReceber() {
        if (this.regime === "CLT") {
            return this.salarioMensal;
        } else if (this.regime === "Horista") {
            return this.horasTrabalhadas * this.valorHora;
        } else if (this.regime === "PJ") {
            return this.valorContrato;
        } else {
            throw new Error("Regime de pagamento inválido.");
        }
    }

    exibirValorAReceber(valorAReceber) {
        console.log("Nome do professor: " + this.nome);
        console.log("Valor a receber: R$ " + valorAReceber.toFixed(2));
    }

    setSalarioMensal(salarioMensal) {
        this.salarioMensal = salarioMensal;
    }

    setHorasTrabalhadas(horasTrabalhadas) {
        this.horasTrabalhadas = horasTrabalhadas;
    }

    setValorHora(valorHora) {
        this.valorHora = valorHora;
    }

    setValorContrato(valorContrato) {
        this.valorContrato = valorContrato;
    }
}

const readline = require('readline');
const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

rl.question("Digite o nome do professor: ", function(nome) {
    rl.question("Digite o regime de pagamento (CLT, Horista ou PJ): ", function(regime) {
        const professor = new Professor(nome, regime);

        if (regime === "CLT") {
            rl.question("Digite o salário mensal do professor: ", function(salarioMensal) {
                try {
                    professor.setSalarioMensal(parseFloat(salarioMensal));
                    const valorAReceber = professor.calcularValorAReceber();
                    professor.exibirValorAReceber(valorAReceber);
                } catch (error) {
                    console.log("Valor inválido inserido. Certifique-se de digitar um número válido.");
                } finally {
                    rl.close();
                }
            });
        } else if (regime === "Horista") {
            rl.question("Digite o número de horas trabalhadas: ", function(horasTrabalhadas) {
                rl.question("Digite o valor da hora de trabalho: ", function(valorHora) {
                    try {
                        professor.setHorasTrabalhadas(parseFloat(horasTrabalhadas));
                        professor.setValorHora(parseFloat(valorHora));
                        const valorAReceber = professor.calcularValorAReceber();
                        professor.exibirValorAReceber(valorAReceber);
                    } catch (error) {
                        console.log("Valor inválido inserido. Certifique-se de digitar um número válido.");
                    } finally {
                        rl.close();
                    }
                });
            });
        } else if (regime === "PJ") {
            rl.question("Digite o valor do contrato do professor: ", function(valorContrato) {
                try {
                    professor.setValorContrato(parseFloat(valorContrato));
                    const valorAReceber = professor.calcularValorAReceber();
                    professor.exibirValorAReceber(valorAReceber);
                } catch (error) {
                    console.log("Valor inválido inserido. Certifique-se de digitar um número válido.");
                } finally {
                    rl.close();
                }
            });
        } else {
            console.log("Regime de pagamento inválido.");
            rl.close();
        }
    });
});
