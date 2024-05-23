# Uml_Gestion_Hotel_Exercice - Diagrammes UML

## 1- Diagramme des cas d’utilisation - Diagramme use case :
@startuml
actor Client
actor ReservationAgent

usecase "Create Hotel" as UC1
usecase "Modify Hotel" as UC2
usecase "View Availability" as UC3
usecase "Make Reservation" as UC4
usecase "Confirm Reservation" as UC5
usecase "Client Check-In" as UC6
usecase "Record Consumption" as UC7
usecase "Generate Invoice" as UC8
usecase "Print Reports" as UC9

Client -- UC3
Client -- UC4
Client -- UC5
Client -- UC6

ReservationAgent -- UC3
ReservationAgent -- UC4
ReservationAgent -- UC5

UC1 -- UC2 : includes
UC3 -- UC4 : extends
UC4 -- UC5 : includes
UC6 -- UC7 : includes
UC7 -- UC8 : includes
@enduml
![Capture d’écran (385)](https://github.com/ilierrazi00/Uml_Gestion_Hotel_Exercice/assets/94292513/65164a1c-7f74-4f04-9980-84bc46843fb8)

## 2- Diagramme de classe UML :
@startuml
class Hotel {
  int id
  String nom
  String adresse
  String telephone
  int classe
  int nombreDeChambres
  + ajouterChambre()
  + modifierChambre()
  + consulterDisponibilités()
}

class Chambre {
  int id
  int numero
  String categorie
  int capacite
  String confort
  float prix
  + estDisponible()
  + reserver()
  + enregistrerConsommation()
}

class Reservation {
  int id
  String codeClient
  String numeroReservation
  Date dateReservation
  Date periodeSejour
  float arrhes
  + confirmer()
  + annuler()
  + enregistrerArrivee()
}

class Client {
  int id
  String nom
  String adresse
  String telephone
  String email
  + effectuerReservation()
  + annulerReservation()
}

class Consommation {
  int id
  String type
  String description
  float prix
  Date date
  + ajouter()
  + supprimer()
}

Hotel "1" -- "n" Chambre
Chambre "1" -- "n" Reservation
Client "1" -- "n" Reservation
Reservation "1" -- "n" Consommation
@enduml
![Capture d’écran (386)](https://github.com/ilierrazi00/Uml_Gestion_Hotel_Exercice/assets/94292513/d508af2d-9ed9-4153-bee9-857e1622c113)

## 3- Diagramme d’activité du processus de réservation :
@startuml
start
:Client remplit formulaire de réservation;
if (Demande soluble ?) then (yes)
  :Établir réservation;
  :Enregistrer arrhes;
else (no)
  :Informer client de l'indisponibilité;
endif
stop
@enduml
![Capture d’écran (387)](https://github.com/ilierrazi00/Uml_Gestion_Hotel_Exercice/assets/94292513/c671a3f9-931d-4e27-af5c-f87cf3734b9d)

## 4- Diagramme de séquence du processus de réservation :
@startuml
actor Client
participant "ReservationSystem" as RS
participant "HotelDatabase" as DB

Client -> RS: Remplir formulaire de réservation
RS -> DB: Vérifier disponibilité
DB -> RS: Disponibilité confirmée
RS -> Client: Confirmation de réservation
RS -> DB: Enregistrer réservation
Client -> RS: Payer arrhes
RS -> DB: Enregistrer paiement
@enduml
![Capture d’écran (388)](https://github.com/ilierrazi00/Uml_Gestion_Hotel_Exercice/assets/94292513/f45abefa-db08-413c-8d8e-2cfac0a54dc9)


