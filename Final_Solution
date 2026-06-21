#include<iostream>
#include<cstdlib>
using namespace std;

enum enGameChoice { Rock = 1, Paper = 2, Scissor = 3 };
enum enWinner { Player = 1, Computer = 2, Draw = 3 };
struct stRoundInfo
{
	short RoundNumber=0;
	enGameChoice PlayerChoice;
	enGameChoice ComputerChoice;
	enWinner Winner;
	string WinnerName="";
};
struct stGameResult
{
	short GameRounds;
	short PlayerWinTimes;
	short ComputerWinTimes;
	short DrawTimes;
	enWinner GameWinner;
	string WinnerName="";

};
short ReadNumberOfRounds()
{
	short num;
	cout << "Please Enter Number Of Rounds you Want to Play : ";
	cin >> num;

	if (num < 0)
	{
		do {
			cout << endl;
			cout << "Please Enter A POSITIVE Number To Play : ";
			cin >> num;
		} while (num < 0);
	}
	return num;
}
int RandomNumber(int From, int To)
{
	int RandNum = rand() % (To - From + 1) + From;
	return RandNum;
}
enGameChoice GetComputerChoice()
{
	return (enGameChoice)RandomNumber(1, 3);
}
enGameChoice GetPlayerChoice()
{
	short Choice;
	do
	{
		cout << "\nYour Choice: [1]:Rock, [2]:Paper, [3]:Scissors? ";
		cin >> Choice;
	} while (Choice < 1 || Choice > 3);
	return (enGameChoice)Choice;
}
enWinner WhoWinRound(stRoundInfo RoundInfo)
{
	if (RoundInfo.PlayerChoice == RoundInfo.ComputerChoice)
	{
		return Draw;
	}

	switch (RoundInfo.PlayerChoice)
	{
	case Rock:
		return (RoundInfo.ComputerChoice == Paper) ? Computer : Player;

	case Paper:
		return (RoundInfo.ComputerChoice == Scissor) ? Computer : Player;

	case Scissor:
		return (RoundInfo.ComputerChoice == Rock) ? Computer : Player;
	}

	return Draw;
}
enWinner WhoWinGame(short PlayerWinTimes, short ComputerWinTimes)
{
	if (PlayerWinTimes > ComputerWinTimes) return Player;
	else if (ComputerWinTimes > PlayerWinTimes) return Computer;
	else return Draw;
}
string ChoiceName(enGameChoice Choice)
{
	string arrGameChoices[3] = { "Rock", "Paper", "Scissor" };
	return arrGameChoices[Choice - 1];
}
string WinnerName(enWinner Winner)
{
	string Winnername[3] = { "Player", "Computer", "Draw" };
	return Winnername[Winner - 1];
}
void SetWinnerScreenColor(enWinner Winner)
{
	switch (Winner)
	{
	case Player:
		system("color 2F");
		break;
	case Computer:
		system("color 4F");
		break;
	case Draw:
		system("color 6F");
		break;
	}
}
void DisplayRoundResult(stRoundInfo RoundInfo)
{
	cout << "\n____________ Round [" << RoundInfo.RoundNumber << "] ____________\n\n";
	cout << "Player1 Choice: " << ChoiceName(RoundInfo.PlayerChoice) << endl;
	cout << "Computer Choice: " << ChoiceName(RoundInfo.ComputerChoice) << endl;
	cout << "Round Winner   : [" << RoundInfo.WinnerName << "]\n";
	cout << "_________________________________________\n" << endl;
	SetWinnerScreenColor(RoundInfo.Winner);
}
void DisplayGameResult(stGameResult GameResult)
{
	cout << "\nNumber Of Rounds: " << GameResult.GameRounds << endl;
	cout << " Player Wins : " << GameResult.PlayerWinTimes << endl;
	cout << " Computer Wins : " << GameResult.ComputerWinTimes << endl;
	cout << " Draw Times : " << GameResult.DrawTimes << endl;
	cout << "\t\t Game Winner    :   " << GameResult.WinnerName;
	SetWinnerScreenColor(GameResult.GameWinner);

}
stGameResult PlayGame(short HowManyRounds)
{
	stRoundInfo RoundInfo;
	short Player1WinTimes = 0, ComputerWinTimes = 0, DrawTimes = 0;

	for (short GameRound = 1; GameRound <= HowManyRounds; GameRound++)
	{
		cout << "\nRound [" << GameRound << "] begins:\n";
		RoundInfo.RoundNumber = GameRound;
		RoundInfo.PlayerChoice = GetPlayerChoice();
		RoundInfo.ComputerChoice = GetComputerChoice();
		RoundInfo.Winner = WhoWinRound(RoundInfo);
		RoundInfo.WinnerName = WinnerName(RoundInfo.Winner);

		if (RoundInfo.Winner == enWinner::Player)
			Player1WinTimes++;
		else if (RoundInfo.Winner == enWinner::Computer)
			ComputerWinTimes++;
		else
			DrawTimes++;

		DisplayRoundResult(RoundInfo);
	}

	return { HowManyRounds, Player1WinTimes, ComputerWinTimes, DrawTimes, WhoWinGame(Player1WinTimes, ComputerWinTimes), WinnerName(WhoWinGame(Player1WinTimes, ComputerWinTimes)) };
}

void StartGame()
{
	char PlayAgain = 'Y';

	do
	{
		system("cls");
		stGameResult GameResults = PlayGame(ReadNumberOfRounds()); 
		cout << "\nGame Over! Winner: " << GameResults.WinnerName << endl;

		cout << "\nDo you want to play again? (Y/N): ";
		cin >> PlayAgain;

	} while (PlayAgain == 'Y' || PlayAgain == 'y');
}
int main()
{
	srand((unsigned)time(NULL));
	StartGame();
	return 0;
}
