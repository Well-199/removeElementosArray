const cozinhas = await Cozinhas.nomes()

        let json = []
        const setCozinha = new Set()

        for(let i in cozinhas){

            let letter = cozinhas[i].nome[0].normalize('NFD').replace(/[\u0300-\u036f]/g, "")

            if(letter==letter){

                json.push({
                    title: letter,
                    cozinha: cozinhas.filter(item => item.nome[0].normalize('NFD').replace(/[\u0300-\u036f]/g, "")==cozinhas[i].nome[0].normalize('NFD').replace(/[\u0300-\u036f]/g, ""))
                })

            }  

        }

        // Limpa os repetidos
        const newJson = json.filter((cozinha) => {
            const cozinhasDuplicadas = setCozinha.has(cozinha.title)
            setCozinha.add(cozinha.title)
            return !cozinhasDuplicadas
        })

        res.json({data: true, result: newJson})
        
        --------------------------------------------------------------------------------
        
        
        <FlatList
                data={categoria}
                keyExtractor={(item) => JSON.stringify(item.title)}
                renderItem={({item}) =>

                <View style={style.categoriaContainer}>
                    
                    <Text style={style.txtAlphabet}>{item.title}</Text>

                    <View style={style.box}>

                        {item.cozinha.map(value => 
                        <TouchableWithoutFeedback onPress={selectCategoria}>
                        
                            <View style={[style.chip]}> 

                                <Text style={[style.textChip]}>
                                    {value.nome}
                                </Text>
                                
                            </View>

                        </TouchableWithoutFeedback>
                        )}

                    </View> 

                </View>
            }>
            </FlatList>
