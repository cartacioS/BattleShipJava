# BattleShipJava

import javax.swing.JOptionPane;

/**
 *
 * @author Katherine
 */
public class BattleshipGame 
{
    public static void main(String args[]) 
    {        
        //Creates a Battleship object
        Battleship game = new Battleship();
        boolean play;
        
        //If the user choses to play, begin a game of Battleship.
        play = play();
        while (play) 
        {
            game = new Battleship();
            //While less than 6 turns have passed and less than 4 hits have 
            //occured, continue.
            for (int i = 0; i < 5 && game.hits() < 4; i++) 
            {
                int one = -2;
                int two = -2;
                
                //Grabs the row of the players target
                do 
                {
                    //For the first prompt that asks the user for the row 
                    //do not display the transcript with past guesses.
                    if (i == 0) 
                    {
                        String guess = JOptionPane.showInputDialog("Please input"
                                + " row value " + "between 1 and 5");
                        int num = Integer.parseInt(guess);
                        if (num > 0 && num < 6) 
                        {
                            one = num - 1;
                        } 
                        else
                        {
                            JOptionPane.showMessageDialog(null, "Try Again!"
                                    + "\nNumber entry must be between 1 and 5",
                                    "Invalid Entry", JOptionPane.ERROR_MESSAGE);
                        }
                    }
                    //Else display the transcript
                    else 
                    {
                        String guess = JOptionPane.showInputDialog("Please input"
                                + " row value " + "between 1 and 5"
                                + game.getTranscript());
                        int num = Integer.parseInt(guess);
                        if (num > 0 && num < 6) 
                        {
                            one = num - 1;
                        } 
                        else 
                        {
                            JOptionPane.showMessageDialog(null, "Try Again!"
                                    + "\nNumber entry "
                                    + "must be between 1 and 5", "Invalid Entry"
                                    + game.getTranscript(),
                                    JOptionPane.ERROR_MESSAGE);
                        }
                    }
                } while (one == -2);

                //Grabs the column of the players target
                do 
                {
                    //For the first prompt that asks the user for the column
                    //do not display the transcript with past guesses.
                    if (i == 0)
                    {
                            String guess = JOptionPane.showInputDialog("Please "
                                    + "input column value between 1 and 5");
                        int num = Integer.parseInt(guess);
                        if (num > 0 && num < 6) 
                        {
                            two = num - 1;
                        } 
                        else 
                        {
                            JOptionPane.showMessageDialog(null, "Try Again!"
                                    + "\nNumber entry must be between 1 and 5", 
                                    "Invalid Entry", JOptionPane.ERROR_MESSAGE);
                        }
                    }
                    
                    //Else display the transcript of past guesses
                    else
                    {
                        String guess = JOptionPane.showInputDialog("Please input"
                                + " column value between 1 and 5" 
                                + game.getTranscript());
                        int num = Integer.parseInt(guess);
                        if (num > 0 && num < 6) 
                        {
                            two = num - 1;
                        } 
                        else 
                        {
                            JOptionPane.showMessageDialog(null, "Try Again!"
                                    + "\nNumber entry must be between 1 and 5" 
                                    + game.getTranscript(), "Invalid Entry",
                                    JOptionPane.ERROR_MESSAGE);
                        }
                    }
                } while (two == -2);

                game.guess(one, two);
            }

            //Displays the boards current state
            game.print();

            if (game.hits() == 4) 
            {
                JOptionPane.showMessageDialog(null, "VITORY! You have "
                        + "Won the War!!", "Game Won", JOptionPane.INFORMATION_MESSAGE);
            } else {
                JOptionPane.showMessageDialog(null, "Sorry, you lost.\nYou "
                        + "found " + game.hits() + " of 4 ship locations.",
                        "Game Lost", JOptionPane.INFORMATION_MESSAGE);
            }
            
            play = playAgain();

        }

        JOptionPane.showMessageDialog(null, "Thank you for your service!");
        //Displays the final state of the board, revealing hidden ships location
        //and players stats
        game.stats();

    }
    
//************************Helper Methods**************************************//
        //Creates a Battleship object
        Battleship game = new Battleship();
        //Method that prompts the user to deicide whether or not they want
        //to play
        private static boolean play()
        {
         boolean contin = false;
        
        //Creates an array of strings "Attack" to play and "Retreat" to quit.
        String[] options = {"Attack", "Retreat"};

        //Asks the user if they would like to begin playing or quit.
        int play = JOptionPane.showOptionDialog(null, "Would you like to "
                + "start a battle?", "BATTLESHIP",
                JOptionPane.DEFAULT_OPTION, JOptionPane.PLAIN_MESSAGE, null,
                options, options[1]);

        if (play == JOptionPane.YES_OPTION)
        {
        String name = JOptionPane.showInputDialog("Please enter your name: ");
        JOptionPane.showMessageDialog(null, "Welcome, Commander " + name + "!\n\n" +
                "The goal of the game is to find the 4  hidden ships,\n"
                + " the output section will display a 5x5 board with your "
                + "attempted attacks.\n"
                + "\t0 = empty spaces \n"
                + "\t2 = sunken ships \n"
                + "\t3 = missed shot "
                + "\nYou will have a total of 5 attacks."
                + "\nGood Luck In Battle!");
        
        System.out.println("Board Key:");
        System.out.println("\t 0 = empty spaces \n \t 1 = surviving ships "
                + "\n \t 2 = sunken ships \n \t 3 = missed attempts\n");
        contin = true;
        }
        return contin;
    }
        
        
    //Method that prompts user to decide whether or not they want to play again
    private static boolean playAgain()
    {
        int play = JOptionPane.showConfirmDialog(null, "Do you want "
                + "to play again?");
        if(play == 0)
        {
            return true;
        }
        else
            return false;
    }   
    

}
