Cirkeluppgiften
===============

Cirkeluppgift

package 
{
	import flash.display.Sprite;
	import flash.events.Event;
	import flash.events.KeyboardEvent;
	import flash.events.MouseEvent;
	import flash.external.ExternalInterface;
	import flash.text.TextField;
	
	/**
	 * ...
	 * @author Ammar
	 */
	public class Main extends Sprite 
	{
		private const MAX_NUMBER_OF_CIRCLES:int = 19;
	
		private var circles:Vector.<Sprite> = new Vector.<Sprite>;
		private var scoreText:TextField;
		private var score:Number;
		private var bomb:Sprite = new Sprite();
		private var spaceIsDown:Boolean;
		
		
		public function Main():void 
		{
			if (stage) init();
			else addEventListener(Event.ADDED_TO_STAGE, init);
		}
		
		private function init(e:Event = null):void 
		{
			removeEventListener(Event.ADDED_TO_STAGE, init);
			
			score = 0;
			scoreText = new TextField();
			scoreText.x = 50;
			addChild(scoreText);
			updateScore();
			
			for (var i:int = 0; i < MAX_NUMBER_OF_CIRCLES; i++) 
			{
				var cir:Sprite = new Sprite();
				cir.graphics.beginFill(Math.random() * 0x0000FF);
				cir.graphics.drawCircle(0, 0, 30);
				cir.graphics.endFill();
				cir.x = Math.random() * stage.stageWidth - cir.width;
				cir.y = Math.random() * stage.stageHeight - cir.height;
				stage.addChild(cir);
				
				cir.addEventListener(MouseEvent.CLICK, Hej);
				circles.push(cir);
			}
			
			bomb.graphics.beginFill(Math.random() * 0xFFFFFF);
			bomb.graphics.drawCircle(0, 0, 50);
			bomb.graphics.endFill();
			stage.addChild(bomb);
			bomb.addEventListener(MouseEvent.CLICK, bombClick);
			
			bomb.x = Math.random() * stage.stageWidth - bomb.width;
			bomb.y = Math.random() * stage.stageHeight - bomb.height;
				
		
			stage.addEventListener(KeyboardEvent.KEY_DOWN, Reset);
			stage.addEventListener(Event.ENTER_FRAME, gameLoop);
		}
		
		private function nyaCirklar():void 
		{
			for (var i:int = 0; i < MAX_NUMBER_OF_CIRCLES; i++) 
			{
				var cir:Sprite = new Sprite();
				cir.graphics.beginFill(Math.random() * 0x0000FF);
				cir.graphics.drawCircle(0, 0, 30);
				cir.graphics.endFill();
				cir.x = Math.random() * stage.stageWidth - cir.width;
				cir.y = Math.random() * stage.stageHeight - cir.height;
				stage.addChild(cir);
				
				cir.addEventListener(MouseEvent.CLICK, Hej);
				circles.push(cir);
			}
		}
		
		private function gameLoop(e:Event):void 
		{
			spawnCircle();
		}
		
		private function spawnCircle():void 
		{
			for (var i:int = 0; i < circles.length; i++) 
			{
				if (spaceIsDown == true) 
				{
					circles[i].visible = true;
				}
			}
		}
		
		private function Reset(e:KeyboardEvent):void 
		{
			if (e.keyCode == 32) 
			{
				// 20 nya cirklar
				nyaCirklar();
				// poäng nollställs
				score = 0;
				scoreText.text = "Score: 0";
			}
		}
		
		private function bombClick(e:MouseEvent):void 
		{
			for (var i:int = 0; i < MAX_NUMBER_OF_CIRCLES; i++) 
			{
				circles[i].x = 8000;
				bomb.visible = false;
			}
		}
		
		private function updateScore():void 
		{
			scoreText.text = "Score: " + score;
		}
		
		private function Hej(e:MouseEvent):void 
		{
			
			Sprite(e.target).visible = false;
			score++;
			updateScore();
			
		}
		
		
	}
	
}
