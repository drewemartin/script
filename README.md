function ChallengeObj(){
		this.natOrder = new Array();
		this.organize = function(val,result){this.natOrder.push(result); this[val]=result};
		this.alphabetize = function(){
			var clean_strings = this.natOrder;
			for(var i = 0; i < clean_strings.length; i++){
				clean_strings[i] = clean_strings[i].replace(/\W/g, '');
			}
			clean_strings.sort();
			for(var i = 0; i < clean_strings.length; i++){
				console.log(this[clean_strings[i]]);
			};
			
		}
		this.regPrint = function(){
			for(var i = 0; i < this.natOrder.length; i++){
				console.log(this.natOrder[i])
			}
		}
	}
	
	var s = "(id,created,employee(id,first,employeeType(id),lastname,location)";
	function solveChallenge(str, alpha){
		
		if(typeof(alpha) !== 'boolean'){
			alpha = false;
		}
		
		var alpha_ary = new Array();
		
		var splitter = 'id';
		var split = str.replace(/[()]/g,'').split(splitter);
		split.shift();
		
		for(var i = 0; i < split.length; i++){
			
			printable = new ChallengeObj();
			
			var current = (splitter + split[i]).split(',');
			for(var n = 0; n < current.length; n++){
				
				if( i === 2 && n === 2){
					printable.organize(current[n], current[n])
					//printable[current[n]] = current[n]
				}else if( i === 2 && n === 1){
					r = '- ' + current[n]
					printable.organize(current[n], r)
					//printable[current[n]] = '- ' + current[n]
				}else{
					r = i > 0 ? (new Array(i + 1).join('-') + ' ' + current[n]) : current[n]
					printable.organize(current[n], r)
				}
			}
			
			if(alpha){
				console.log('here')
				var to_push = printable.natOrder;
				for(var x = 0; x < to_push.length; x++){
					alpha_ary.push(to_push[x])
				}
			}else{
				printable.regPrint();
			}
		}
		if(alpha){
			alpha_ary.sort();
			for(var i = 0; i < alpha_ary.length; i++){
				console.log(alpha_ary[i]);
			}
		}
	}
