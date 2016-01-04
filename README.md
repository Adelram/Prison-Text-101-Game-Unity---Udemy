using UnityEngine;
using UnityEngine.UI;
using System.Collections;

public class TextController : MonoBehaviour {
	
	public Text Text;
	
	//This boolean will check whether or not we have the Mirror.
	public bool Mirror_item;
	
	//Privates
	private enum States {cell, mirror, sheets, lock_0, freedom};
	private States MyState;
	
	// Use this for initialization
	void Start () {
		MyState = States.cell;
	
	}
	
	// Update is called once per frame
	void Update () {
		print (MyState);
		if (MyState == States.cell) 					{state_cell();} 
		else if (MyState == States.sheets) 				{state_sheet();}
		else if (MyState == States.mirror) 				{state_mirror();}
		else if (MyState == States.lock_0) 				{state_lock_0();} 
		else if (MyState == States.freedom) 			{state_freedom();}		
	}
	
	//States are found from this point downwards.
	void state_cell (){
		if (Mirror_item == true) {
			Text.text = "You are in your prison cell, " +
						"with a mirror in your hand.\n\n" +
						"Press S to view Sheets or L to view Lock.";
			if (Input.GetKeyDown(KeyCode.S)) 			{MyState = States.sheets;}
			else if (Input.GetKeyDown(KeyCode.L))		{MyState = States.lock_0;}
		}
			else if (Mirror_item == false) {
				Text.text = "You are in  prison cell, and you want to escape. There are " +
							"some dirty sheets in front on the bed, a mirror on the wall, and the door " +
							"is locked from the inside.\n\n" +
							"Press S to view Sheets, M to view Mirror or L to view Lock.";
				if (Input.GetKeyDown(KeyCode.S)) 		{MyState = States.sheets;}
				else if (Input.GetKeyDown(KeyCode.M)) 	{MyState = States.mirror;}
				else if (Input.GetKeyDown(KeyCode.L)) 	{MyState = States.lock_0;}
		}
	}
		
	void state_sheet (){
		if (Mirror_item == true) {
			Text.text = "Holding a mirror in hand doesn't make the sheets look any better.\n\n " +
						"Press R to Return to roaming your cell.";
			if (Input.GetKeyDown(KeyCode.R)) 			{MyState = States.cell;}
			}
			else if (Mirror_item == false) {	
				Text.text = "You can't believe you slept in these things. Surely it's " +
							"Time somebody changed them. Ahh, the pleasures of prison life I guess!\n\n" +
							"Press R to Return to roaming your cell.";
				if (Input.GetKeyDown(KeyCode.R)) 		{MyState = States.cell;}
			}
		
	}
	
	void state_mirror (){
		if (Mirror_item == false) {
			Text.text = "You observed the mirror and find something strange behind it." +
						"You decided to take the item behind the mirror.\n\n" +
						"Press T to take the mirror or R to Return to roaming your cell.";
			if (Input.GetKeyDown(KeyCode.T)) {
				Text.text = "You took the mirror with you.\n\n" +
							"Press R to return to roaming your cell.";
				Mirror_item = true;
			} else if (Input.GetKeyDown(KeyCode.R)) 	{MyState = States.cell;}
		}	
		else if (Input.GetKeyDown(KeyCode.R)) 			{MyState = States.cell;}			
	}				
	
	void state_lock_0 (){
		if (Mirror_item == true) {
					Text.text = "You carefully put the mirror through the bars, and turn it around " +
								"so you can see the lock. You can just make out fingerprints around " + 
								"the buttons. You press the dirty buttons, and hear a click.\n\n" +
								"Press O to Open or R to Return to roaming your cell.";
			if (Input.GetKeyDown(KeyCode.O))			{MyState = States.freedom;}
				else if (Input.GetKeyDown(KeyCode.R))	{MyState = States.cell;}
		}
			else if (Mirror_item == false) {
					Text.text = "This is one of those button locks. You have no idea what the ." +
								"Combination is. You wish you could somehow see where the dirty " +
								"fingerprints were, maybe that would help. \n\n" +
								"Press R to Return to roaming your cell.";
			if (Input.GetKeyDown(KeyCode.R))			{MyState = States.cell;}
			}
		else if (Input.GetKeyDown(KeyCode.R))			{MyState = States.cell;}	
	}
	
	void state_freedom () {
		Text.text = "Congratulations! You have seized your freedom!\n\n" +
					"Press P to play again!";
		if (Input.GetKeyDown(KeyCode.P)) 				{MyState = States.cell;}
		Mirror_item = false;
	}	
}

