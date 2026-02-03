# GroupProject9
USE ns_Sp25_21482_Group9;

###Tables 1 & 2
#Tickets & Ticket Sales, Tickets contribute to Ticket Sales
##Types of Tickets Ex. 1-Day pass, 2-Day Pass, Animal Encounter, etc.
#Ticket Sales contributes to Profits & Expenses
CREATE TABLE Ticket_Types(
	typeOfTicket VARCHAR(25), 
    amountPerTicket DECIMAL(4,2),
    ticketDescription VARCHAR(85),
    PRIMARY KEY (typeOfTicket)
    );
    
CREATE TABLE Ticket_Sales(
	tSaleDate DATE, 
    amountSold INT,
    typeOfTicket VARCHAR(25),
    PRIMARY KEY(tSaleDate),
    CONSTRAINT TSalesHasTickets FOREIGN KEY(typeOfTicket) REFERENCES Ticket_Types(typeOfTicket)
    );
 
###Table 3
#Section of the Zoo, contributes to Enclosures
CREATE TABLE Section(
	sectionName VARCHAR(25), 
    sectionTheme VARCHAR(45),
    sectionLocation VARCHAR(85),
    PRIMARY KEY(sectionName)
    );

###Table 4    
#Enclosures (found within Sections, each has 1 or more animals within), Contributes to Resident Animal
	CREATE TABLE Enclosure(
	enclosureID VARCHAR(9), 
    enclosureType VARCHAR(45),
    sectionName VARCHAR(25),
    PRIMARY KEY(enclosureID),
    CONSTRAINT enclosureHasSection FOREIGN KEY(sectionName) REFERENCES Section(sectionName)
    );

###Table 5    
#Food Source, contributes to Food Type
 CREATE TABLE Food_Source(
	foodSource VARCHAR(45), 
    pricePerUnit DECIMAL(4,2),
    PRIMARY KEY (foodSource)
    );
 
###Table 6 
#Food Type, gets info from Food Source, Contributes to Species
CREATE TABLE Food_Type(
	foodType VARCHAR(45), 
    foodSource VARCHAR(45),
    PRIMARY KEY(foodType),
    CONSTRAINT foodHasSource FOREIGN KEY(foodSource) REFERENCES Food_Source(foodSource)
    );

###Table 7
#Food transactions
  CREATE TABLE Food_Purchases(
	foodPurchaseDate DATE, 
    foodAmountBought DECIMAL(8.2),
    foodSource VARCHAR(45),
    PRIMARY KEY(foodPurchaseDate),
    CONSTRAINT PurchaseHasSource FOREIGN KEY(foodSource) REFERENCES Food_Source(foodSource)
    );

###Table 8
#Vet Needs, contributes to species
CREATE TABLE Vet_Needs(
	vetProcedure VARCHAR(45), 
    procedureDescription VARCHAR(85),
    procedureCost DECIMAL(4,2),
    PRIMARY KEY (vetProcedure)
    );

###Table 9
#Species
CREATE TABLE Animal_Species(
	species VARCHAR(45),
    speciesType VARCHAR(45),
    foodType VARCHAR(45),
    vetProcedure VARCHAR(45),
    PRIMARY KEY (species),
    CONSTRAINT speciesNeedsVet FOREIGN KEY(vetProcedure) REFERENCES Vet_Needs(vetProcedure),
    CONSTRAINT speciesNeedsFood FOREIGN KEY(foodType) REFERENCES Food_Type(foodType)
    );

###Table 10
#Vet Transaction
CREATE TABLE Vet_Transactions(
	vetOperationDate DATE, 
	animalID VARCHAR(9),
    PRIMARY KEY(vetOperationDate),
    CONSTRAINT animalHadOperation FOREIGN KEY(animalID) REFERENCES Resident_Animal(animalID)
    );

##Table 11
#Resident Animal, Contributes to Employees and Events
    CREATE TABLE Resident_Animal(
	animalID VARCHAR(9), 
    animalName VARCHAR(45),
    species VARCHAR(45),
    enclosureID VARCHAR(9), 
    PRIMARY KEY(animalID),
    CONSTRAINT animalHasEnclosure FOREIGN KEY(enclosureID) REFERENCES Enclosure(enclosureID),
    CONSTRAINT animalHasSpecies FOREIGN KEY(species) REFERENCES Animal_Species(species)
    );

###Table 12
#Employees, each is assigned to an animal
CREATE TABLE ZooEmployees(
	employeeNumber VARCHAR(9), 
    employeeName VARCHAR(45),
    employeeFname VARCHAR(13),
    employeeLname VARCHAR(45),
    yearsEmployed INT,
    animalID VARCHAR(9),
    PRIMARY KEY (employeeNumber),
    CONSTRAINT animalHasEmployee FOREIGN KEY(animalID) REFERENCES Resident_Animal(animalID)
    );

###Table 13    
#Zoo Events
##Each event would have an animal, employees participating would be connected through the animal. 
CREATE TABLE ZooEvents(
    zooEvent VARCHAR(45),
    eventDescription VARCHAR(100),
    animalID VARCHAR(9),
    PRIMARY KEY(zooEvent),
    CONSTRAINT eventHasAnimal FOREIGN KEY(animalID) REFERENCES Resident_Animal(animalID)
    );
    
###Table 14
#Date, used to calculate transactions
CREATE TABLE Transaction_Dates(
	MMDDYEAR DATE,
   	PRIMARY KEY (MMDDYEAR), 
	CONSTRAINT datehasfoodtransaction FOREIGN KEY(MMDDYEAR) REFERENCES Ticket_Sales(tSaleDate),
   	CONSTRAINT datehasticketsales FOREIGN KEY(MMDDYEAR) REFERENCES Food_Purchases(foodPurchaseDate),
 	CONSTRAINT datehasvettransaction FOREIGN KEY(MMDDYEAR) REFERENCES Vet_Transactions(vetOperationDate)
	);
