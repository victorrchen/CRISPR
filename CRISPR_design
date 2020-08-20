"""Checks if the input is indeed a valid DNA sequence, and outputs true if so."""
def DNA_check(DNA):
	seq = list("ATCGatcgnN")
	for n in DNA:
		a = n in seq
		if a == False:
			return False
	return True


"""Input a nucleotide and outputs the reverse complement of that nucleotide."""
def reverse_nucleotide(n):
	if n == "A" or n == "a":
		return "t"
	if n == "C" or n == "c":
		return "g"
	if n == "G" or n == "g":
		return "c"
	if n == "T" or n == "t":
		return "a"
	if n == "N" or n == "n":
		return "n"

"""Reverses the string."""
def reverse_string(s):
	string = ""
	for i in s:
		string = i + string
	return string



"""Produces the reverse complement of the DNA sequence entered."""
def reverse_comp(DNA):
	rc = ""
	for n in DNA:
		rc += reverse_nucleotide(n)

	return reverse_string(rc)


"""Input your DNA sequence of choice and outputs a list of guide RNAs, but only in one direction."""
def guide(DNA):
	counter = 0
	gRNA = ""
	final = []
	for n in DNA:
		gRNA += n
		counter += 1
		if counter == 33:
			if gRNA[31:] == "gg":
				final.append((gRNA[0:30]))
				gRNA = gRNA[1:]
				counter -= 1
			else:
				gRNA = gRNA[1:]
				counter -= 1
	return final

"""Input a DNA sequence and outputs a series of gRNAs both in forward and reverse directions, with overhangs,
ready for IDT ordering."""
def crispr(DNA):
	if DNA_check(DNA):

		if len(DNA) < 33:
			print("Please enter a sequence longer than 32 bases.")
			return

		DNA = DNA.lower()
		DNA_rev = reverse_comp(DNA)
		if len(guide(DNA)) == 0 and len(guide(DNA_rev)) == 0:
			print("No guides found.")
			return
		print("Forward guides: ")

		for F_guides in guide(DNA):
			print(("5'- AAAC" + F_guides + "G- 3'", "5'- AAAAC" + reverse_comp(F_guides) + "- 3'"))
			if "ggtctc" in F_guides or "gagacc" in F_guides:
				print("WARNING, BsaI cut site exists in the guide above.")

		print("Reverse guides: ")
		for R_guides in guide(DNA_rev):
			print(("5'- AAAC" + R_guides + "G- 3'", "5'- AAAAC" + reverse_comp(R_guides) + "- 3'"))
			if "ggtctc" in R_guides or "gagacc" in R_guides:
				print("WARNING, BsaI cut site exists in the guide above.")

		return
	else:
		print("Must enter valid sequence.")
		return
