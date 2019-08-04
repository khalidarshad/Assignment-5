#include "Card.h"
#include "Player.h" //is this bad?

extern Player* currentPlayer; //the current player
extern vector<Player> players; //all the other players 
extern Card* getCardByName(string cardName);

Card::Card() {
	//this->name = cardName;
	//this->price = cardPrice; 
}

//Generic card copy constructor
Card::Card(const Card& other) {
	
	this->name = other.getName();
	this->price = other.getPrice();
}

Card::Card(string cardName, int cardPrice) {
	this->name = cardName;
	this->price = cardPrice;
}

//Base class mutators and accessors
string Card::getName() const {
	return name;
}

int Card::getPrice() const {
	return this->price;
}

string Card::getType() const {
	return this->type;
}

void Card::setName(string cardName) {
	this->name = cardName;
}
void Card::setPrice(int cardPrice){
	this->price = cardPrice;
}

Copper::Copper() {
	this->value = 1;
	this->name = "Copper";
	this->price = 0;
	this->type = "Treasure";
}

int Copper::getValue() {
	return this->value;
}

Silver::Silver() {
	this->value = 1;
	this->name = "Silver";
	this->price = 3;
	this->type = "Treasure";
}

int Silver::getValue() {
	return this->value;
}

Gold::Gold() {
	this->value = 3;
	this->name = "Gold";
	this->price = 6;
	this->type = "Treasure";
}

int Gold::getValue() {
	return this->value;
}

Estate::Estate() {
	this->victoryPoints = 1;
	this->name = "Estate";
	this->price = 2;
	this->type = "Victory";
}

int Estate::getVictoryPoints() {
	return this->victoryPoints;
}

Duchy::Duchy() {
	this->victoryPoints = 3;
	this->name = "Duchy";
	this->price = 5;
	this->type = "Victory";
}

int Duchy::getVictoryPoints() {
	return this->victoryPoints;
}

Province::Province() {
	this->victoryPoints = 6;
	this->name = "Province";
	this->price = 8;
	this->type = "Victory";
}

int Province::getVictoryPoints() {
	return this->victoryPoints;
}
//Cellar card
Cellar::Cellar() { 
	this->name = "Cellar";
	this->price = 2;
	this->type = "Action";
	this->description = "+1 Action\nDiscard any number of cards, then draw that many.";
}

void Cellar::execute(){
	//terminal specific picker
	std::cout << "Enter the names of any cards you wish to discard" << std::endl;
	std::cout << "enter \"done\" when done"<< std::endl;
	while(true) {
		std::string choice; 
		std::cin >> choice;
		Card* pickedCard = getCardByName(choice);	
		if( pickedCard != NULL ) {
			currentPlayer->discardCard(pickedCard);
			currentPlayer->drawCards(1);
		}
		if(choice == "done"){
			break;
		}
	}
	currentPlayer->addActions(1);
}

string Cellar::getDescription() {
	return this->description;
}

//chapel card
Chapel::Chapel() { 
	this->name = "Chapel";
	this->price = 2;
	this->type = "Action";
	this->description = "Trash up to 4 cards from your hand."; 
}

void Chapel::execute(){
	//terminal specific picker
	std::cout << "Enter the names of any cards in your hand you wish to trash (up to 4)" << std::endl;
	std::cout << "enter \"done\" when done"<< std::endl;
	int numTrashed = 0;
	while(numTrashed < 4) {
		std::string choice; 
		std::cin >> choice;
		Card* pickedCard = getCardByName(choice);	
		if( pickedCard != NULL ) {
			currentPlayer->trashCard(pickedCard);
			numTrashed++;
		}
		if(choice == "done"){
			break;
		}
	}
}

string Chapel::getDescription() {
	return this->description;
}

//moat card
Moat::Moat() { 
	this->name = "Moat";
	this->price = 2;
	this->type = "Action - Reaction";
	this->description = "+2 Cards;\nWhen another player plays an\nAttack card, you may reveal this\nfrom your hand. If you do, you are\nunaffected by that Attack."; 
}

void Moat::execute(){
	currentPlayer->drawCards(2);
	//TODO: Finish this function
}

string Moat::getDescription() {
	return this->description;
}


//chancellor card
Chancellor::Chancellor() { 
	this->name = "Chancellor";
	this->price = 3;
	this->type = "Action";
	this->description = "+$2\nYou may immediately put your deck into your discard pile.";
}

void Chancellor::execute(){
	currentPlayer->addMoney(2);
	//terminal specific picker
	std::cout << "do you want to put your deck into your discard pile? (Enter \"yes\" or \"no\")" << std::endl;
	while(true) {
		std::string choice; 
		std::cin >> choice;
		if(choice == "yes"){
			currentPlayer->discardDeck();
			break;
		}
		if(choice == "no"){
			break;
		}
	}
}

string Chancellor::getDescription() {
	return this->description;
}

//village card
Village::Village() { 
	this->name = "Village";
	this->price = 3;
	this->type = "Action";
	this->description = "+1 Card; +2 Actions."; 
}

void Village::execute(){
	currentPlayer->drawCards(1);
	currentPlayer->addActions(2);
}

string Village::getDescription() {
	return this->description;
}

//woodcutter card
Woodcutter::Woodcutter() { 
	this->name = "Woodcutter";
	this->price = 3;
	this->type = "Action";
	this->description = "+1 Buy; +$2."; 
}

void Woodcutter::execute(){
	currentPlayer->addBuys(1);
	currentPlayer->addMoney(2);
}

string Woodcutter::getDescription() {
	return this->description;
}

//workshop card
Workshop::Workshop() { 
	this->name = "Workshop";
	this->price = 3;
	this->type = "Action";
	this->description = "Gain a card costing up to $4."; 
}

void Workshop::execute(){
	//terminal specific picker
	while(true) {
		std::cout << "Enter the name of a card costing up to $4." << endl;
		std::string choice;
		std::cin >> choice;
		Card* pickedCard = getCardByName(choice);
		if(pickedCard != NULL) { //make sure it's a real card
			if(pickedCard->getPrice() <= 4) {
				int cardLocation = -1; 
				for(int i = 0; i < board.size(); ++i) {
					if(board.at(i)->getName() == pickedCard->getName()){
						cardLocation = i; //find the right card
					}
				}
				if( cardLocation >= 0 ) {
					currentPlayer->addToDiscard(board.at(cardLocation)); //add card to discard pile
					board.erase( board.begin() + cardLocation);//remove from gameboard
				}
				break;						
			}
		}
	}
}

string Workshop::getDescription() {
	return this->description;
}

//feast card
Feast::Feast() { 
	this->name = "Feast";
	this->price = 4;
	this->type = "Action";
	this->description = "Trash this card. Gain a card\ncosting up to $5."; 
}

void Feast::execute(){
	currentPlayer->trashCard(getCardByName("Feast"));
	//terminal specific picker
	while(true) {
		std::cout << "Enter the name of a card costing up to $5." << endl;
		std::string choice;
		std::cin >> choice;
		Card* pickedCard = getCardByName(choice);
		if(pickedCard != NULL) { //make sure it's a real card
			if(pickedCard->getPrice() <= 5) {
				int cardLocation = -1; 
				for(int i = 0; i < board.size(); ++i) {
					if(board.at(i)->getName() == pickedCard->getName()){
						cardLocation = i; //find the right card
					}
				}
				if( cardLocation >= 0 ) {
					currentPlayer->addToDiscard(board.at(cardLocation)); //add card to discard pile
					board.erase( board.begin() + cardLocation);//remove from gameboard
				}
				break;						
			}
		}
	}
}

string Feast::getDescription() {
	return this->description;
}

//moneylender card
Moneylender::Moneylender() { 
	this->name = "Moneylender";
	this->price = 4;
	this->type = "Action";
	this->description = "Trash a Copper from your hand. If\nyou do, +$3.";
}

void Moneylender::execute(){
	if(currentPlayer->cardInHand(getCardByName("Copper"))) { 
		currentPlayer->trashCard(getCardByName("Copper"));
		currentPlayer->addMoney(3);	
	}
}

string Moneylender::getDescription() {
	return this->description;
}

//remodel card
Remodel::Remodel() { 
	this->name = "Remodel";
	this->price = 4;
	this->type = "Action";
	this->description = "Trash a card from your hand. Gain\na card costing up to $2 more than\nthe trashed card.";
}

void Remodel::execute(){
	//terminal specific picker
	while(true) {
		std::cout << "Enter the name of a card in your hand you wish to trash" << std::endl;
		std::string choice; 
		std::cin >> choice;
		Card* pickedCard = getCardByName(choice);	
		if(pickedCard != NULL) {
			if( currentPlayer->cardInHand(pickedCard) ) {
				currentPlayer->trashCard(pickedCard);
				while(true) {
					std::cout << "Enter the name of a card costing up to $2 more" << std::endl;
					std::cin >> choice;
					Card* cardToGain = getCardByName(choice);	
					if(cardToGain != NULL) {
						if(cardToGain->getPrice() <= (pickedCard->getPrice() + 2)) {
							int cardLocation = -1; 
							for(int i = 0; i < board.size(); ++i) {
								if(board.at(i)->getName() == cardToGain->getName()){
									cardLocation = i; //find the right card
								}
							}
							if( cardLocation >= 0 ) {
								currentPlayer->addToDiscard(board.at(cardLocation)); //add card to discard pile
								board.erase( board.begin() + cardLocation);//remove from gameboard
							}
							break;
						}
					}
				}
				break;
			}
		}
	}
}

string Remodel::getDescription() {
	return this->description;
}

//smithy card
Smithy::Smithy() { 
	this->name = "Smithy";
	this->price = 4;
	this->type = "Action";
	this->description = "+3 Cards.";
}

void Smithy::execute(){
	currentPlayer->drawCards(3);
}

string Smithy::getDescription() {
	return this->description;
}

//throne room card
Throneroom::Throneroom() { 
	this->name = "Throneroom"; //having a space in the name messes it up
	this->price = 4;
	this->type = "Action";
	this->description = "Choose an Action card in your\nhand. Play it twice.";
}

void Throneroom::execute(){
	while(true) {
		std::cout << "Enter the name of an Action card in your hand to be played twice. Otherwise enter \"done\"" << endl;
		std::string choice;
		std::cin >> choice;
		Card* pickedCard = getCardByName(choice);
		if(pickedCard != NULL) { //make sure it's a real card
			if(pickedCard->getType().substr(0,6) == "Action") { 
				if(pickedCard->getType() != "Throneroom") { //you cant play Throneroom again
					currentPlayer->playAction(pickedCard);
					currentPlayer->playAction(pickedCard);
					break;
				}

			}
		}
		if(choice == "done") {
			break; //in case the player has no other action cards, let them stop
		}
	}
}

string Throneroom::getDescription() {
	return this->description;
}

//councilroom card
Councilroom::Councilroom() { 
	this->name = "Councilroom";
	this->price = 5;
	this->type = "Action";
	this->description = "+4 Cards; +1 Buy\nEach other player draws a card.";
}

void Councilroom::execute(){
	currentPlayer->drawCards(4);
	currentPlayer->addBuys(1);

	for(int i = 0; i < players.size(); ++i) {
		if(players.at(i).getName() != currentPlayer->getName()) {
			players.at(i).drawCards(1); //make every other player draw a card.
		}
	} 
	
}

string Councilroom::getDescription() {
	return this->description;
}

//festival card
Festival::Festival() { 
	this->name = "Festival";
	this->price = 5;
	this->type = "Action";
	this->description = "+2 Actions, +1 Buy, +$2.";
}

void Festival::execute(){
	currentPlayer->addActions(2);
	currentPlayer->addBuys(1);
	currentPlayer->addMoney(2);
}

string Festival::getDescription() {
	return this->description;
}

//laboratory card
Laboratory::Laboratory() { 
	this->name = "Laboratory";
	this->price = 5;
	this->type = "Action";
	this->description = "+2 Cards; +1 Action."; 
}

void Laboratory::execute(){
	currentPlayer->drawCards(2);
	currentPlayer->addActions(1);
}

string Laboratory::getDescription() {
	return this->description;
}

//library card
Library::Library() { 
	this->name = "Library";
	this->price = 5;
	this->type = "Action";
	this->description = "Draw until you have 7 cards in\nhand. You may set aside any\nAction cards drawn this way, as\nyou draw them; discard the set aside cards after you finish drawing."; 
}

void Library::execute(){
	while(currentPlayer->getHand().size() < 7) {
		currentPlayer->drawCards(1);
	}
}

string Library::getDescription() {
	return this->description;
}
