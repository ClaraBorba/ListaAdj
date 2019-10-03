# ListaAdj
Segundo exercício de grafos


import java.io.IOException;

public class Main {
    public static void main(String [] args) {
        try{
            ListaAdjacente lista = new ListaAdjacente(args[0]);
        } catch (IOException e) {
            System.out.println(e.getMessage());
        }
    }
}











import java.io.*;
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

public class ListaAdjacente {
    private String nomeArq;
    private List<List<Integer>> lista;
    private char vertices;  // Número de vértices.
    private int grau[];   // Vetor que guarda o grau de cada vértice;

    public ListaAdjacente(String nomeArq) throws IOException{
        this.nomeArq = nomeArq;
        confirmaArq();
        listando();
        printLista();
    }

    private void confirmaArq() throws IOException {
        File arq = new File(nomeArq);
        if(!arq.exists()) {
            throw new IOException("Arquivo não existente");
        }
    }

    private void inicializa(int tamanho) {
        lista = new ArrayList<>(tamanho);
        for(int i = 0; i < tamanho; i++) {
            lista.add(i, new ArrayList<Integer>());
        }
    }

    private void listando() {
        String linha;
        int valor;
        int x = 0;

        try(BufferedReader bf = new BufferedReader(new InputStreamReader(new FileInputStream(nomeArq)))) {
            Scanner s;
            s = new Scanner(bf.readLine());
            inicializa(s.nextInt());
            while ((linha = bf.readLine()) != null) {
                s = new Scanner(linha);
                while (s.hasNext()) {
                    valor = s.nextInt();
                    if (valor != -1) {
                        lista.get(x).add(valor);
                    }
                }
                x++;
            }

        } catch(EOFException e1) { // faz nada }
        } catch (IOException e) {
            System.out.println("O Arquivo não conseguiu ser lido.");
        }
    }

    private void printLista() {
        for(List<Integer> l : lista) {
            System.out.print("v[]: ");
            for(int i : l) {
                System.out.print(i+" ");
            }
            System.out.println();
        }
    }
}


