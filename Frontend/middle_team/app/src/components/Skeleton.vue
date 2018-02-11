<template>
  <div class="skeleton">

    <header class="head">
        <div class="head__logo">
            <!--<img src="../assets/logo.png" alt="Logo">-->
        </div>
        <div class="head__export">
            <i class="fa fa-cloud-download fa-2x" aria-hidden="true"></i>
            <button @click="exportFunction()">Export</button>
        </div>
        <img class="head__avatar" src="../assets/elvis.jpg" alt="Avatar">
    </header>

    <div class="main_container">
        <nav>
            <div class="sections-menu">
                <ul>
                    <li>
                      <a href="">ΕΠΙΧΕΙΡΗΜΑΤΙΚΟ ΜΟΝΤΕΛΟ</a>
                      <ul>
                        <router-link to="/2a-identity" tag="li" class="">
                          <a>ΤΑΥΤΟΤΗΤΑ</a>
                        </router-link>
                        <router-link to="/2b-description" tag="li" class="">
                          <a>ΠΕΡΙΓΡΑΦΗ</a>
                        </router-link>
                      </ul>
                    </li>
                    <li>
                      <a href="">ΑΝΑΛΥΣΗ ΑΓΟΡΑΣ</a>
                      <ul>
                        <router-link to="/market-general" tag="li" class="">
                          <a>Γενικές</a>
                        </router-link>
                      </ul>
                    </li>
                    <!-- <li>
                        <a href="">ΕΠΙΧΕΙΡΗΜΑΤΙΚΟ ΜΟΝΤΕΛΟ</a>
                        <ul>
                            <li>
                                <a href="">ΤΑΥΤΟΤΗΤΑ</a>
                            </li>
                            <li>
                                <a href="">ΠΕΡΙΓΡΑΦΗ</a>
                            </li>
                        </ul>
                    </li>
                    <li>
                        <a href="">ΑΝΘΡΩΠΙΝΟ ΔΥΝΑΜΙΚΟ</a>
                        <ul>
                            <li>
                                <a href="">ΟΜΑΔΑ ΔΙΟΙΚΗΣΗΣ</a>
                            </li>
                            <li>
                                <a href="">ΠΡΟΣΩΠΙΚΟ</a>
                            </li>
                            <li>
                                <a href="">ΕΞΩΤΕΡΙΚΟΙ ΣΥΝΕΡΓΑΤΕΣ</a>
                            </li>
                            <li>
                                <a href="">ΑΝΑΛΥΣΗ ΚΟΣΤΟΥΣ</a>
                            </li>
                        </ul>
                    </li>
                    <li>
                        <a href="">ΕΓΚΑΤΑΣΤΑΣΕΙΣ - ΕΞΟΠΛΙΣΜΟΣ</a>
                        <ul>
                            <li>
                                <a href="">ΤΟΠΟΣ ΕΓΚΑΤΑΣΤΑΣΗΣ</a>
                            </li>
                            <li>
                                <a href="">ΕΞΟΠΛΙΣΜΟΣ</a>
                            </li>
                            <li>
                                <a href="">ΑΝΑΛΥΣΗ ΚΟΣΤΟΥΣ</a>
                            </li>
                        </ul>
                    </li>
                    <li>
                        <a href="">ΠΡΟΪΟΝΤΑ - ΥΠΗΡΕΣΙΕΣ</a>
                        <ul>
                            <li>
                                <a href="">ΠΡΟΙΟΝΤΑ - ΥΠΗΡΕΣΙΕΣ</a>
                            </li>
                            <li>
                                <a href="">ΠΝΕΥΜΑΤΙΚΗ ΙΔΙΟΚΤΗΣΙΑ</a>
                            </li>
                            <li>
                                <a href="">ΑΝΑΛΥΣΗ ΕΣΟΔΩΝ</a>
                            </li>
                        </ul>
                    </li>
                    <li>
                        <a href="">ΑΝΑΛΥΣΗ ΑΓΟΡΑΣ</a>
                        <ul>
                            <li>
                                <a href="">ΑΝΑΛΥΣΗ SWOT</a>
                            </li>
                            <li>
                                <a href="">ΑΝΑΛΥΣΗ PESTEL</a>
                            </li>
                            <li>
                                <a href="">ΓΕΝΙΚΕΣ ΠΑΡΑΤΗΡΗΣΕΙΣ</a>
                            </li>
                        </ul>
                    </li>
                    <li>
                        <a href="">ΣΤΡΑΤΗΓΙΚΗ MARKETING</a>
                        <ul>
                            <li>
                                <a href="">ΣΤΡΑΤΗΓΙΚΗ</a>
                            </li>
                            <li>
                                <a href="">ΕΝΕΡΓΕΙΕΣ MARKETING</a>
                            </li>
                        </ul>
                    </li>
                    <li>
                        <a href="">ΧΡΗΜΑΤΟΙΚΟΝΟΜΙΚΟΣ ΣΧΕΔΙΑΣΜΟΣ</a>
                        <ul>
                            <li>
                                <a href="">ΚΟΣΤΟΣ ΕΝΑΡΞΗΣ</a>
                            </li>
                            <li>
                                <a href="">ΚΟΣΤΟΣ ΛΕΙΤΟΥΡΓΙΑΣ</a>
                            </li>
                            <li>
                                <a href="">ΝΕΚΡΟ ΣΗΜΕΙΟ</a>
                            </li>
                        </ul>
                    </li>
                    <li>
                        <a href="">ΧΡΟΝΟΔΙΑΓΡΑΜΜΑ</a>
                    </li>
                    <li>
                        <a href="">ΠΑΡΑΡΤΗΜΑ</a>
                    </li>
                    <li>
                        <a href="">ΣΥΝΟΨΗ</a>
                    </li> -->

                </ul>
            </div>
        </nav>

        <main>
            <router-view/>
        </main>
    </div>

    <footer class="foot">
        <button class="foot__back">ΠΙΣΩ</button>
        <span class="foot__pagination">
            <p>1/2</p>
        </span>
        <button class="foot__next">ΜΠΡΟΣΤΑ</button>
    </footer>
    
  </div>
</template>

<script>

import pdfMake from "pdfmake/build/pdfmake"
import pdfFonts from "pdfmake/build/vfs_fonts"
pdfMake.vfs = pdfFonts.pdfMake.vfs

export default {
 	name: 'Skeleton',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  methods: {
  	// This function returns a parsed date from the db form(YYYYMMDD) into proper form with slashes(DD/MM/YYYY)
  	dateParser(date){
  		return String(date).slice(6) + "/" 
	 			+ String(date).slice(4, 6) + "/"
	 			+ String(date).slice(0, 4)
  	},
					fourProductsFun(db) {
						var charListArray = []
						var charListArrayObj=db["products"]
						for (var i = 0; i < charListArrayObj.length; i++) {
							if(db.products[i].ProductType){
								var productType="Προϊόν: "
							}
							else{
								var productType="Υπηρεσία: "
							}
							charListArray.push([{text: productType + charListArrayObj[i].Name},
											{text: "Απευθυνόμενο σε: " + charListArrayObj[i].Directed_to},
											{text: "Σχέδιο Καινοτομίας: " + charListArrayObj[i].Innovation_factor},
											{text: "Τεχνολογία: " + charListArrayObj[i].Technology},
											{text: "Απαιτήσεις Άδειας: " + charListArrayObj[i].Certificate},
											{text: "Άδεια: " + charListArrayObj[i].License},
											{text:"Ανταγωνισμός: " + charListArrayObj[i].Competition},
											{text: "Τελική Τιμή: " + charListArrayObj[i].Price + "€"},
											{text: "Περιγραφή: " + charListArrayObj[i].Description}, " "])
						}
						return charListArray
					},
					fiveTwoPestelFun(db) {
						var factorsArray = []
						var factorsArrayObj = db["factors"]
						for (var i = 0; i < factorsArrayObj.length; i++){
							factorsArray.push([{text: "Περιγραφή: " + factorsArrayObj[i].Description},
										{text: "Παράδειγμα: " + factorsArrayObj[i].Example}, " "])
						}
						return factorsArray	
					},
					sixTwoMarketingFun(db) {
						var marketingActionsArray = []
						var marketingActionsArrayObj = db["marketingActions"]
						for (var i = 0; i < marketingActionsArrayObj.length; i++){
							marketingActionsArray.push([{text: "Ενέργεια: " + marketingActionsArrayObj[i].Title},
											{text: "Χρόνος Υλοποίησης: " + marketingActionsArrayObj[i].ImplementationTime},
											{text: "Συχνότητα: " + marketingActionsArrayObj[i].Frequency},
											{text: "Κόστος Υλοποίησης: " + marketingActionsArrayObj[i].ImplementationCost},
											{text: "Συνολικό Κόστος: " + marketingActionsArrayObj[i].TotalCost}, " "])
						}
						return marketingActionsArray	
					},
    exportFunction(){
    	var db = this.$store.state
			// PDFMake code here
			var docDefinition = {
				// Content of the pdf document
				content: [
					// Section 1
					{text: "Επιχειρηματικό Μοντέλο", style: "sectionHeader"},
					" ",
					// Subsection 1.1
					// This content element is a complicated one, with extra "tags" like bold, underline, etc., all contained into the style. 
					// Notice it is inside curly brackets.
					{text: "1.1 Ταυτότητα Επιχείρησης:", style: "subSectionHeader"},
					" ", // Newline
					// This content element is a simple string element, no need for curly brackets, just comma after it.
					"Όνομα επιχείρησης: " 		 + db.identity[0].Name,
					"Ημερομηνία δημιουργίας: " + this.dateParser(db.identity[0].Date),
					"Νομική μορφή: " 		       + db.identity[0].LegalForm,
					"Τύπος επιχείρησης: "      + db.identity[0].OrderOfBusiness,
					" ",
					// Section 4
					{text: "Προϊόντα - Υπηρεσίες", style: "sectionHeader"},
					" ",
					{ol: this.fourProductsFun(db)},
					" "," ",
					// Section 5
					{text: "Ανάλυση Αγοράς", style: "sectionHeader", pageBreak: "before"},
					" ",
					// Section 5.1
					{text: "5.1 Ανάλυση SWOT:", style: "subSectionHeader"},
					" ",
					{columns: [
						{
							width: '50%',
							stack: [
								"Δυνατά: ",
								{
									ul: db["swot"][0].Strong
								}
							]
						},
						{
							width: '50%',
							stack: [
								"Αδύναμα: ",
								{
									ul: db["swot"][0].Weak
								}
							]
						},
					]},
					" ",
					{columns: [
						{
							width: '50%',
							stack: [
								"Ευκαιρίες: ",
								{
									ul: db["swot"][0].Opportunities
								}
							]
						},
						{
							width: '50%',
							stack: [
								"Απειλές: ",
								{
									ul: db["swot"][0].Threats
								}
							]
						}
					]},
					" ",

					// Section 5.2
					{text: "5.2 Ανάλυση PESTEL:", style: "subSectionHeader"},
					" ",
					{ol: this.fiveTwoPestelFun(db)},
	 				" "," ",
					// Section 5.3
					{text: "5.3 Γενικές Παρατηρήσεις:", style: "subSectionHeader"},
					" ",
					{text: db["note"][0].Text},
	 				" "," ",
					// Section 6
					{text: "Στρατηγική Marketing", style: "sectionHeader"},
					" ",
					// Section 6.1	
					{text: "6.1 Στρατηγική:", style: "subSectionHeader"},
					" ",
					"Κανάλια Προβολής: " 			  + db["strategy"][0].Promotion,
					"Κανάλια Διανομής: " 			  + db["strategy"][0].Contribution,
					"Τεχνικές Εισαγωγής στην Αγορά: " + db["strategy"][0].MarketEntry,
					"Δημόσιες Σχέσεις: "              + db["strategy"][0].PublicRelations,
					"Κινήσεις προς Αποφυγείν: "       + db["strategy"][0].Avoid,
	 				" "," ",
					// Section 6.2
					{text: "6.2 Ενέργειες Marketing:", style: "subSectionHeader"},
					" ", 
					{ol: this.sixTwoMarketingFun(db)},
	 				" "," ", 
					
				], // Content array end

				styles: {
				    sectionHeader: {
				      bold: true, underline: true, fontSize: 20, alignment: "left", decoration:"underline"
				    },
				    subSectionHeader: {
				      bold: true, underline: true, fontSize: 15, alignment: "left", decoration:"underline"
				    }
				  }

			} // docDefinition end
			
			// Download the PDF, named after the business name given in section 1.1
			pdfMake.createPdf(docDefinition).download(db.identity[0].Name + "BusinessPlan.pdf");
    } // ExportFun end		
  }
}
</script>

<style>
        /* APP */

        .skeleton {
            display: flex;
            flex-direction: column;
            justify-content: initial;
            align-items: stretch;
            min-height: 100vh;
        }


        /* HEADER */

        .head {
            background-color: rgb(30, 33, 51);
            display: flex;
            justify-content: space-between;
            align-items: center;
            height: 80px;
            ;
        }

        .head__logo {
            margin-left: 20px;
        }

        .head__export {
            color: #fff;
            display: flex;
            margin-right: 100px;
            align-items: center;
        }


        .head__avatar {
            height: 70px;
            width: 70px;
            border-radius: 50%;
            margin-right: 20px;
        }

        .head__export p {
            margin-left: 5px;
            font-size: 20px;
        }

        .head__export i {}


        /* FOOTER */

        footer {
            background-color: rgb(203, 202, 202);
            height: 60px;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .foot__back {
            margin-right: 30px;
            background-color: rgb(41, 152, 88);
            color: white;
            width: 100px;
            height: 40px;
            display: flex;
            justify-content: center;
            align-items: center;
            border-style: none;
        }

        .foot__next {
            margin-left: 30px;
            background-color: rgb(41, 152, 88);
            color: white;
            width: 100px;
            height: 40px;
            display: flex;
            justify-content: center;
            align-items: center;
            border-style: none;
        }

        .foot__pagination {
            font-size: 20px;
            font-weight: 600;
            color: black;
        }


        main {
            flex-grow: 1;
        }

        .main_container {
            flex-grow: 1;
            display: flex;
            justify-content: space-between;
            align-items: stretch;
        }

        nav {
            background-color: rgb(30, 33, 51);
            width: 350px;
        }


        /* SECTIONS MENU */

        .sections-menu {}

        .sections-menu ul {
            list-style: none;
            margin: 0;
        }

        .sections-menu ul li {
            padding: 15px;
            position: relative;
            width: 350px;
            border-top: 1px solid black;
            background-color: rgb(30, 33, 51);
        }

        .sections-menu ul li {
            border-right: 5px solid rgb(61, 65, 90);
        }

        .sections-menu ul ul {
            opacity: 0;
            position: absolute;
            visibility: hidden;
            left: 100%;
            top: -2%;
            background-color: rgb(40, 44, 63);
        }

        .sections-menu ul ul li {
            background-color: rgb(79, 84, 115);
            width: 250px;
        }

        .sections-menu ul li:hover ul {
            opacity: 1;
            visibility: visible;
        }

        .sections-menu ul li a {
            color: white;
        }


        /* BASIC ELEMENTS */

        .basic_button {
            background-color: rgb(24, 146, 105);
            width: 100px;
            height: 40px;
            display: flex;
            justify-content: center;
            align-items: center;
        }
    </style>
