#include <iostream>
#include <iomanip>
#include <vector>
#include <string>
#include <algorithm>
#include <cmath>

#include <opengm/opengm.hxx>
#include<opengm/graphicalmodel/graphicalmodel.hxx>
#include<opengm/graphicalmodel/space/simplediscretespace.hxx>
#include<opengm/functions/potts.hxx>
#include<opengm/operations/adder.hxx>

    

using namespace opengm; 
using namespace std;


const size_t nx = 30; // width of the grid 
const size_t ny = 30; // height of the grid 
const size_t numberOfLabels = 2; 
double lambda = 0.1; // coupling strength of the Potts model 


// this function maps a node (x, y) in the grid to a unique variable index 
inline size_t variableIndex(const size_t x, const size_t y) 
{ 
	return (x+nx + y);
}

int main()
{

	typedef SimpleDiscreteSpace<size_t, size_t> Space;// Construye el Label Space
	Space space(nx * ny, numberOfLabels);

	//typedef GraphicalModel<double, opengm::Adder, OPEMGM_TYPELIST_2(ExplicitFunction<double, PottsFunction<double>), Space> Model;//crea un graphical model type
  	typedef opengm::GraphicalModel<float, opengm::Adder,ExplicitFunction<double>,opengm::SimpleDiscreteSpace<> > Model;

	Model gm(space);

	//Añadir a cada nodo(x,y) en la rejilla

	for(size_t y=0;y< ny;++y)
	{
		for(size_t x=0;x< nx;++x)
		{
			const size_t shape[]={numberOfLabels};
			ExplicitFunction<double> f(shape, shape+1);//Declara funcion a usar
			for(size_t s=0;s< numberOfLabels;++s)
			{
				f(s)=(1.0 - lambda)*rand()/RAND_MAX;
			}

			Model::FunctionIdentifier fid = gm.addFunction(f);

			size_t variableIndices[] = {variableIndex(x,y)};
			gm.addFactor(fid, variableIndices, variableIndices+1);
		}


 	}


	return 0;
		

} 








