# batalla

package batalla;
    
import javax.swing.JOptionPane;
import java.util.Scanner;

public class Batalla {
    
    
    public static void imprimir(int m[][]){
		for(int i = 0; i < m.length; i++){
			for (int j = 0; j < m.length; j++) {
				System.out.print(m[i][j]+" ");
			}
			System.out.print("\n");
		}
		System.out.print("\n");
	}

	public static void main(String []args){

		Scanner sc = new Scanner(System.in);

		String aux;
		
		aux = JOptionPane.showInputDialog(null, "Ingrese el tamaño del juego: ");
		int tamaño = Integer.parseInt(aux);

		aux = JOptionPane.showInputDialog(null, "Ingrese la cantidad de barcos por jugador: ");
		int cant_barcos = Integer.parseInt(aux);


		int [][] m1 = new int [tamaño][tamaño];
		int [][] m2 = new int [tamaño][tamaño];


		for(int i = 0; i < tamaño; i++){
			for (int j = 0; j < tamaño; j++) {
				m1 [i][j] = 0;
				m2 [i][j] = 0;
			}
		}


		int jugador = 0;
		while (jugador < 2){
			for (int i = 0; i < cant_barcos; i++) {
				aux = JOptionPane.showInputDialog(null, "JUGADOR "+(jugador+1)+"\nIngrese la cordenada (x) del barco "+(i+1)+": ");
				int x = Integer.parseInt(aux);
				while(x<0 || x > tamaño-1){
					aux = JOptionPane.showInputDialog(null,"Valor ingresado invalido, intente nuevamente: ");
					x = Integer.parseInt(aux);
				}
			
				aux = JOptionPane.showInputDialog(null, "JUGADOR "+(jugador+1)+"\nIngrese la cordenada (y) del barco "+(i+1)+": ");
				int y = Integer.parseInt(aux);
				while(y<0 || y > tamaño-1){
					aux = JOptionPane.showInputDialog(null,"Valor ingresado invalido, intente nuevamente: ");
					y = Integer.parseInt(aux);
				}

				if(jugador == 0){
					m1 [y][x] = 1;
				}
				else{
					m2 [y][x] = 1;
				}
			}
			jugador++;
		}
		//imprimir(m1);
		//imprimir(m2);

		int barcos1 = cant_barcos, barcos2 = cant_barcos;

		boolean termino = false, turno1 = true, turno2 = false;
		while (termino == false){
			if(turno1 == true && termino == false){
				System.out.print("\nDISPARA EL JUGADOR 1\nIngrese la cordenada (x) del barco que desea destruir: ");
				int x = sc.nextInt();
				while(x < 0 || x > tamaño-1){
					System.out.print("Valor ingresado invalido, intenta nuevamente: ");
					x = sc.nextInt();
				}
				System.out.print("\nIngrese la cordenada (y) del barco que desea destruir: ");
				int y = sc.nextInt();
				while(y < 0 || y > tamaño-1){
					System.out.print("Valor ingresado invalido, intenta nuevamente: ");
					y = sc.nextInt();
				}

				if(m2[y][x] == 1){
					System.out.print("\n| Barco hundido |\n");
					m2[y][x] = 0;
					barcos2--;
					
					imprimir(m2);
					
					if (barcos2 == 0){
						termino = true;
					}
				}
				else{
					System.out.print("\n| Siga participando |\n");
				}
				turno1 = false;
				turno2 = true;

			}
			else if (turno2 == true && termino == false){
				System.out.print("\nDISPARA EL JUGADOR 2\nIngrese la cordenada (x) del barco que desea destruir: ");
				int x = sc.nextInt();
				while(x < 0 || x > tamaño-1){
					System.out.print("Valor ingresado invalido, intenta nuevamente: ");
					x = sc.nextInt();
				}

				System.out.print("\nIngrese la cordenada (y) del barco que desea destruir: ");
				int y = sc.nextInt();
				while(y < 0 || y > tamaño-1){
					System.out.print("Valor ingresado invalido, intenta nuevamente: ");
					y = sc.nextInt();
				}

				if(m1[y][x] == 1){
					System.out.print("\n| Barco hundido |\n");
					m1[y][x] = 0;
					barcos1--;
					
					imprimir(m1);
					
					if(barcos1 == 0){
						termino = true;
					}
				}
				else{
					System.out.print("\n| Siga participando :c |\n");
				}
				turno2 = false;
				turno1 = true;

			}
		}
		System.out.print("\n|El juego a finalizado|\n");
	}
}

