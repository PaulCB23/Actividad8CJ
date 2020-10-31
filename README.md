# Actividad8CJ
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Scanner;

public class Act8Java {

    public static void main(String [] args) throws IOException{
        Scanner sc = new Scanner(System.in);
        BufferedReader lector = new BufferedReader(new InputStreamReader(System.in));
        Deck deck = new Deck();
        int opcion;
        String repetir;
        do{
            System.out.println("Juego de Poker \nBuena Suerte! \nEscoja una de las siguientes opciones:  ");
            System.out.println("1) Mezclar deck\n2) Sacar una carta\n3) Carta al azar \n4) Generar una mano de 5 cartas\n0) salir");
            opcion = sc.nextInt();

            switch(opcion){
                case 1:
                    System.out.println("Mezclar deck");
                    deck.shuffle();
                    break;
                case 2:
                    System.out.println("Sacar una carta");
                    deck.head();
                    break;
                case 3:
                    System.out.println("Sacar una carta al azar");
                    deck.pick();
                    break;
                case 4:
                    System.out.println("Mano de 5 cartas");
                    System.out.println(deck.hand().toString());
                    break;
                case 0:
                    System.out.println("Gracias por jugar");
                    System.exit(opcion);
                    break;
            }System.out.println("Repetir el menu?\n si o no");
            repetir = lector.readLine();
        }while(repetir.equals("si"));

    }

}

import java.util.ArrayList;
import java.util.Collections;

public class Deck {

    public ArrayList deck = new ArrayList();
    public ArrayList handOfFive = new ArrayList();

    public Deck (){
        Card card = new Card();
        for(int i = 0; i < card.getPalo().size(); i++) {
            for(int k = 0; k < card.getValor().size(); k++) {
                if(card.getPalo().get(i) == "treboles"){
                    deck.add("{" + card.getPalo().get(i) + ", " + card.getColor().get(1) + ", " + card.getValor().get(k) + "}");
                }
                if(card.getPalo().get(i) == "picas"){
                    deck.add("{" + card.getPalo().get(i) + ", " + card.getColor().get(1) + ", " + card.getValor().get(k) + "}");
                }
                if(card.getPalo().get(i) == "corazones"){
                    deck.add("{" + card.getPalo().get(i) + ", " + card.getColor().get(0) + ", " + card.getValor().get(k) + "}");
                }
                if(card.getPalo().get(i) == "diamantes"){
                    deck.add("{" +card.getPalo().get(i)  + ", " + card.getColor().get(0)  + ", " +  card.getValor().get(k) + "}");
                }

            }
        }
    }
    public void shuffle () {
        Collections.shuffle(deck);
        System.out.println("Se mezclo el Deck");
    }
    public void head(){
        System.out.println(deck.get(0));
        deck.remove(0);
        System.out.println("Quedan "+ deck.size() +" cartas restantes en el deck.");
    }
    public void pick(){
        int range = (int) ((Math.random() * (deck.size() - 1)) + 1);
        System.out.println(deck.get(range));
        deck.remove(range);
        System.out.println("Quedan "+ deck.size() +" cartas restantes en el deck.");
    }
    public ArrayList hand(){
        for(int i = 0; i < 5 ; i ++) {
            handOfFive.add(deck.get(0));
            deck.remove(0);
        }
        System.out.println("Se han tomado 5 cartas y ahora quedan "+ deck.size() +" cartas restantes en el deck.");
        return handOfFive;
    }
}


import java.util.ArrayList;

public class Card {

    private ArrayList palo = new ArrayList();
    private ArrayList color = new ArrayList();
    private ArrayList valor = new ArrayList();

    public Card(){
        palo.add("treboles");
        palo.add("corazones");
        palo.add("picas");
        palo.add("diamantes");
        color.add("rojo");
        color.add("negro");
        for(int i = 2; i <= 10 ; i ++){
            valor.add(i);
        }
        valor.add('A');
        valor.add('J');
        valor.add('Q');
        valor.add('K');
    }
    public ArrayList getPalo() {
        return palo;
    }
    public ArrayList getColor() {
        return color;
    }
    public ArrayList getValor() {
        return valor;
    }
}


