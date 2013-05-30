FinalProject
============
import info.gridworld.actor.Actor;
import info.gridworld.grid.Location;
import java.util.Scanner;

public class RunningBack extends Actor
{
   public void move(String direction)
   {
       Location moveLocation = getLocation();
       if (direction.equals("up"))
       {
           if (this.getLocation().getRow()==0)
               return;
           moveLocation = getLocation().getAdjacentLocation(0);
       }
       else if (direction.equals("right"))
       {
           if (this.getLocation().getCol()==this.getGrid().getNumCols()-1)
               return;
           moveLocation = getLocation().getAdjacentLocation(90);
       }
       else if (direction.equals("down"))
       {
           if (this.getLocation().getRow()==this.getGrid().getNumRows()-1)
               return;
           moveLocation = getLocation().getAdjacentLocation(180);
       }
       else if (direction.equals("left"))
       {
           if (this.getLocation().getCol()==0)
               return;
           moveLocation = getLocation().getAdjacentLocation(270);
       } 
       if (this.getGrid().get(moveLocation) != null || !this.getGrid().isValid(moveLocation))
           return;
       else super.moveTo(moveLocation);      
  }
  
  public void act()
  {
      return;
    }
  

}



import info.gridworld.actor.Critter;
import info.gridworld.grid.Location;
import java.util.ArrayList;
import info.gridworld.actor.Actor;


public class DefensivePlayer extends Critter
{
    public ArrayList<Actor> getActors()
    {
        return null;
    }
    
    public void processActors(ArrayList<Actor> actors)
    {
        return;
    }
}


import info.gridworld.world.World;
import info.gridworld.actor.ActorWorld;
import info.gridworld.grid.BoundedGrid;
import info.gridworld.grid.Grid;
import info.gridworld.grid.Location;
import info.gridworld.gui.WorldFrame;

import java.util.ArrayList;
import java.util.Random;
import java.util.Set;
import java.util.TreeSet;

import javax.swing.JFrame;


public class FootballWorld extends ActorWorld
{
    RunningBack r1 = null;

    public boolean keyPressed(String description, Location loc)
    {
        if (description.equals("W"))
        {
            r1.move("up");
        }
        else if (description.equals("D"))
        {
            r1.move("right");
        }
        else if (description.equals("S"))
        {
            r1.move("down");
        }
        else if (description.equals("A"))
        {
            r1.move("left");
        }
        return true;
    } 

    public void addRunningBack(Location loc, RunningBack theRunningBack)
    {
        super.add(loc, theRunningBack);
        r1 = theRunningBack;
    }
}



import info.gridworld.actor.ActorWorld;
import info.gridworld.actor.Critter;
import info.gridworld.actor.Flower;
import info.gridworld.actor.Rock;
import info.gridworld.grid.Location;

import java.awt.Color;

/**
 * This class runs a world that contains critters. <br />
 * This class is not tested on the AP CS A and AB exams.
 */
public class CritterRunner
{
    public static void main(String[] args)
    {
        FootballWorld world = new FootballWorld();
        world.add(new Location(7, 8), new Rock());
        world.add(new Location(3, 3), new Rock());
        world.add(new Location(2, 8), new Flower(Color.BLUE));
        world.add(new Location(5, 5), new Flower(Color.PINK));
        world.add(new Location(1, 5), new Flower(Color.RED));
        world.add(new Location(7, 2), new Flower(Color.YELLOW));
        world.add(new Location(4, 4), new DefensivePlayer());
        world.add(new Location(5, 6), new DefensivePlayer());
        world.add(new Location(1, 1), new DefensivePlayer());
        world.add(new Location(6, 0), new DefensivePlayer());
        world.addRunningBack(new Location(5, 8), new RunningBack());
        world.show();
    }
}

