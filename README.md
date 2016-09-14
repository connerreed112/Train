# Train
TRAIN CLASS

//FILE :FerryBoat.java
//PROG : Conner Reed
//PURP : To simulate loading and unloading a boat, as well as traveling to different ports

package edu.tridenttech.cpt187.reed.program4;

import java.util.Random;

public class FerryBoat 
{
	private int peopleOnBoard;			
	private int maxCapacity;		
	private int minCapacity;
	private int currentPort;			
	private int numPorts;				
	private int destPort;				
	private Random ranNumGenerator;
	
	public FerryBoat(int portCount, int maxPersons, int startPort, int minPersons)
	{
		numPorts = portCount;
		maxCapacity = maxPersons;
		minCapacity = minPersons;
		currentPort = startPort;
		destPort = currentPort;
		peopleOnBoard = 0;				
		ranNumGenerator = new Random();
	}
	
	public int getPeopleOnBoard()
	{
		
		return peopleOnBoard;
		
	}
	
	public int getMaxCapacity()
	{
		
		return maxCapacity;
				
	}
	
	public int getCurrentPort()
	{
		
		return currentPort;
		
	}
	
	public int getNumPorts()
	{
		
		return numPorts;
		
	}
	
	public int getDestPort()
	{
		
		return destPort;
		
	}
	
	public void moveToPort(int nextPort)
	{
		
		//Starts the loop back at port 1
		if (nextPort > numPorts)
		{
			nextPort = 1;
		}
		
		destPort = nextPort;
		
		System.out.printf("Leaving from port #%d for port #%d with %d passengers.\n", currentPort, destPort, peopleOnBoard);
		
		currentPort = nextPort;
		
	}
	
	public int genRandNumber(int maxNum)
	{
		
		return ranNumGenerator.nextInt(maxNum + 1);
		
	}
	
	public void unloadPeople(int number)
	{
		// If the number of people is more than the number on board, defaults to peopleOnBoard
		if (number > peopleOnBoard)
		{
			number = peopleOnBoard;
		}
		
		//Unloads everyone at the end of trip
		if (destPort == 1)
		{
			number = peopleOnBoard;
		}
		
		peopleOnBoard -= number;
		
		System.out.printf("We have arrived at port #%d!\n", destPort);
		
		System.out.printf("There are " + number + " people leaving the ship.\n");
		
		
	}
	
	public void loadPeople(int number)
	{
		
		
		
		System.out.printf("There are " + number + " people waiting to get on board.\n");
		//Makes sure that there are no more people on board than maxCapacity
		if (peopleOnBoard + number > maxCapacity)
		{
			
			System.out.printf("The boat cannot hold " + (peopleOnBoard + number) + " people, so we will be leaving with the maximum number of people allowed. Sorry folks!");
			
			number = maxCapacity - peopleOnBoard;
		
		}
		
		peopleOnBoard += number;
		
	}
}

MAIN CLASS


package edu.tridenttech.cpt187.reed.program4;

public class Main {

	public static void main(String[] args) 
	{
	
		final int PORTCOUNT = 20;
		FerryBoat myBoat = new FerryBoat(PORTCOUNT, 125, 1, 1);
		myBoat.loadPeople(myBoat.genRandNumber(150));
		
		System.out.println("ALL ABOARD THE SUPER COOL FERRY BOAT!!!!!\n");
		
		for (int ct = 0; ct < PORTCOUNT; ++ct)
		{
			myBoat.moveToPort(myBoat.getCurrentPort() + 1);
			myBoat.unloadPeople(myBoat.genRandNumber(125));
			myBoat.loadPeople(myBoat.genRandNumber(150));
		}
		
		System.out.printf("We have arrived! Thank you for choosing the SUPER COOL FERRY BOAT!\n");
	
	}

}
